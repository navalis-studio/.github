# Observability — Navalis API

## What was implemented

I added a full observability stack to the Navalis backend to monitor application health in real time. The stack consists of:

- **Prometheus** — collects and stores metrics every 5 seconds
- **Grafana** — visual dashboard with 11 panels (auto-refresh every 5s)
- **Zipkin** — distributed tracing (shows the path of each request inside the backend)
- **Loki** — centralized log aggregation (with traceId/spanId correlation)

Everything runs via Docker Compose — a single command brings up the entire infrastructure.

---

## Custom metrics

Beyond the automatic metrics (HTTP latency, JVM memory, threads), I created game-specific metrics:

| Metric | Type | What it measures |
|---|---|---|
| `navalis_players_online` | Gauge | Active players (WebSocket open OR HTTP request < 60s) |
| `navalis_games_active` | Gauge | Games currently in memory |
| `navalis_players_connected` | Gauge | Players with open WebSocket (in-game) |
| `navalis_games_total` | Counter | Total games created since boot |
| `navalis_games_finished_total` | Counter | Total games finished |
| `navalis_shots_fired_total` | Counter | Total shots fired |
| `navalis_shots_hit_total` | Counter | Total hits |
| `navalis_shots_miss_total` | Counter | Total misses |

---

## Distributed tracing

With Zipkin, I can see exactly where each request spends time. For example, a login takes ~105ms, and the trace shows that 103ms are spent on BCrypt hash verification:

```
POST /api/auth/login [total: 105ms]
├── security filterchain before [1ms]
├── authorize request [0.1ms]
├── secured request [103ms]  ← BCrypt hash verification
└── security filterchain after [0.1ms]
```

---

## Load testing (k6)

Two load test scenarios to validate performance under stress:

| Scenario | Description | VUs | Thresholds |
|---|---|---|---|
| Game Simulation | Full cycle (register → lobby → create/join) | up to 100 | p95 < 500ms, error < 5% |
| Polling Stress | Polling endpoints (available games + ranking) | up to 100 | p95 < 500ms, error < 5% |

---

## Technical decisions

### Problem: I need distributed tracing. Which tool to use?

**Alternatives:** OpenTelemetry (OTLP) vs Zipkin

**I chose Zipkin** because Spring Boot 4 has a dedicated starter (`spring-boot-starter-zipkin`) that integrates with Micrometer Tracing out of the box. OpenTelemetry would require an intermediate Collector (one more container in the stack), and for a single-service application Zipkin handles it without that extra complexity.

---

### Problem: How to measure "players online" when the game uses both HTTP and WebSocket?

**Alternatives:** Count only WebSocket connections vs count only HTTP requests vs combine both

**I chose to combine** because WebSocket alone doesn't cover the lobby (a player browsing rooms only makes HTTP requests), and HTTP alone fails during gameplay (a player firing only uses WebSocket). Combining both ensures accurate counting across all game phases.

---

### Problem: The "Players Online" gauge took up to 70 seconds to update after logout.

**Solution:** I created a `POST /api/auth/logout` endpoint that removes the player from the metrics and recalculates the gauge immediately. The frontend calls this endpoint before clearing the token.

---

### Problem: Traces in Zipkin were polluted with irrelevant requests (actuator, swagger, CORS preflight).

**Alternatives:** Filter in Zipkin (UI) vs filter in the application before exporting

**I chose to filter in the application** with an `ObservationPredicate` that ignores infra endpoints (/actuator, /swagger-ui, /v3/api-docs), OPTIONS requests, and Spring Security observations. This way Zipkin only receives traces from actual game requests.

---

### Problem: I need centralized logs to correlate with traces.

**Alternatives:** ELK Stack (Elasticsearch + Logstash + Kibana) vs Grafana Loki

**I chose Loki** because I already have Grafana in the stack — Loki integrates natively as a datasource without needing additional tools. ELK would require 3 extra containers and significantly more memory. I configured the `loki4j` logback appender to send logs with traceId/spanId, allowing me to go from a trace in Zipkin directly to the correlated logs in Grafana.

---

### Problem: I need to validate whether the backend can handle load before going to production.

**Alternatives:** JMeter vs k6 vs Artillery

**I chose k6** because scripts are plain JavaScript (easy to write), it runs lightweight in the terminal, and has detailed output metrics (percentiles, thresholds). I created two scenarios: one that simulates the full player cycle (register → lobby → create/join) with up to 100 simultaneous users, and another that stresses the polling endpoints (available games + ranking). Thresholds require p95 < 500ms and less than 5% error rate.

---

## How to run

```bash
docker compose up --build
```

| Service | URL | Credentials |
|---|---|---|
| Grafana | http://localhost:3000 | admin / admin |
| Zipkin | http://localhost:9411 | — |
| Loki | http://localhost:3000/explore → Loki datasource | — |
| Prometheus | http://localhost:9090 | — |
| Raw metrics | http://localhost:5000/actuator/prometheus | — |
