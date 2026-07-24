<p align="center">
  <img src="https://raw.githubusercontent.com/navalis-studio/.github/main/profile/navalis_logo.png" alt="Navalis" width="200"/>
</p>

<h3 align="center">Online Battleship — Real-Time Strategy</h3>

<p align="center">
  <em>A classic reimagined with 1930s noir aesthetics, real-time duels and competitive ranking.</em>
</p>

<p align="center">
  <a href="https://navalis.vercel.app">Play Now</a> •
  <a href="https://github.com/navalis-studio/navalis-api">Backend</a> •
  <a href="https://github.com/navalis-studio/navalis-web">Frontend</a>
</p>

---

## The Project

**Navalis** is a multiplayer battleship game where two players face off in real time, positioning fleets and firing shots in alternating turns. Sink the entire enemy fleet first to win.

What sets it apart is the experience: an interface inspired by 1930s Rubber Hose cartoons with a Film Noir aesthetic, vintage film effects, animated mascots and cinematic transitions — all running on a modern architecture with WebSocket for instant communication.

## How It Works

```
┌─────────────┐     ┌─────────────────┐     ┌──────────────┐     ┌─────────────┐
│ Create Room │ ──▶ │  Place Fleet    │ ──▶ │   Battle!    │ ──▶ │   Result    │
│  or Join    │     │  (5 ships)      │     │ (20s turns)  │     │  + Ranking  │
└─────────────┘     └─────────────────┘     └──────────────┘     └─────────────┘
```

| Feature | Description |
|---------|-------------|
| ⏱️ Timed turns | 20 seconds per move — hesitate and the system fires for you |
| 🔗 Room codes | Share a 6-character code to play with friends |
| 🏆 Global ranking | Top 20 players by wins, with win/loss rate |
| 🔄 Reconnection | Dropped? You have 30 seconds to rejoin without losing the match |
| 🎬 Cinematic aesthetic | Film grain, iris wipe transitions, animated mascots |

## Architecture

```
                    ┌──────────────────────┐
                    │     navalis-web      │
                    │  React 19 + Vite 8   │
                    │  Tailwind CSS 4      │
                    └──────────┬───────────┘
                               │
                    HTTP (REST) │ WebSocket (STOMP)
                               │
                    ┌──────────▼───────────┐
                    │     navalis-api      │
                    │  Spring Boot 4       │
                    │  Java 21 + JWT       │
                    └──────────┬───────────┘
                               │
                    ┌──────────▼───────────┐
                    │    PostgreSQL 16     │
                    │  (users + results)   │
                    └─────────────────────┘
```

<table>
  <tr>
    <td><strong>Backend</strong></td>
    <td>
      <img src="https://img.shields.io/badge/Java-21-ED8B00?logo=openjdk&logoColor=white" alt="Java 21"/>
      <img src="https://img.shields.io/badge/Spring%20Boot-4.0-6DB33F?logo=springboot&logoColor=white" alt="Spring Boot"/>
      <img src="https://img.shields.io/badge/PostgreSQL-16-4169E1?logo=postgresql&logoColor=white" alt="PostgreSQL"/>
      <img src="https://img.shields.io/badge/WebSocket-STOMP-010101?logo=websocket&logoColor=white" alt="WebSocket"/>
      <img src="https://img.shields.io/badge/JWT-Auth-000000?logo=jsonwebtokens&logoColor=white" alt="JWT"/>
      <img src="https://img.shields.io/badge/Flyway-Migrations-CC0200?logo=flyway&logoColor=white" alt="Flyway"/>
    </td>
  </tr>
  <tr>
    <td><strong>Frontend</strong></td>
    <td>
      <img src="https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black" alt="React 19"/>
      <img src="https://img.shields.io/badge/Vite-8-646CFF?logo=vite&logoColor=white" alt="Vite"/>
      <img src="https://img.shields.io/badge/Tailwind%20CSS-4-06B6D4?logo=tailwindcss&logoColor=white" alt="Tailwind"/>
      <img src="https://img.shields.io/badge/STOMP.js-WebSocket-010101" alt="STOMP.js"/>
    </td>
  </tr>
  <tr>
    <td><strong>Infra</strong></td>
    <td>
      <img src="https://img.shields.io/badge/Vercel-Frontend-000000?logo=vercel&logoColor=white" alt="Vercel"/>
      <img src="https://img.shields.io/badge/Render-Backend-46E3B7?logo=render&logoColor=white" alt="Render"/>
      <img src="https://img.shields.io/badge/Docker-Container-2496ED?logo=docker&logoColor=white" alt="Docker"/>
      <img src="https://img.shields.io/badge/GitHub%20Actions-CI-2088FF?logo=githubactions&logoColor=white" alt="CI"/>
    </td>
  </tr>
</table>

## Repositories

| Repo | Description |
|------|-------------|
| [`navalis-api`](https://github.com/navalis-studio/navalis-api) | REST API + WebSocket STOMP, DDD domain model, JWT auth, unit tests |
| [`navalis-web`](https://github.com/navalis-studio/navalis-web) | Player interface, audio system, animations, auto-reconnection |

## Design: Ink & Iron Noir

Navalis' visual identity is a fusion of three references:

- **Rubber Hose (1930s)** — rounded shapes, squash & stretch animations, Mickey glove mascots
- **Film Noir** — strict monochrome, film grain, vignette, hard shadows
- **Brutalism** — thick borders, hard shadows, bold typography

> Palette: `#131313` · `#000000` · `#FFFFFF` · `#C2C2C2` · `#6E6E6E`

---

<p align="center">
  <strong>Navalis Studio</strong> · Built by <a href="https://github.com/jhowzluk">@jhowzluk</a>
</p>
