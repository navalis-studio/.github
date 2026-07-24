<p align="center">
  <img src="https://raw.githubusercontent.com/navalis-studio/.github/main/profile/navalis_logo.png" alt="Navalis" width="200"/>
</p>

<h3 align="center">Batalha Naval Online — Estratégia em Tempo Real</h3>

<p align="center">
  <em>Um clássico reinventado com estética noir dos anos 30, duelos em tempo real e ranking competitivo.</em>
</p>

<p align="center">
  <a href="https://navalis.vercel.app">🎮 Jogar Agora</a> •
  <a href="https://github.com/navalis-studio/navalis-api">⚙️ Backend</a> •
  <a href="https://github.com/navalis-studio/navalis-web">🎨 Frontend</a>
</p>

---

## O Projeto

**Navalis** é um jogo de batalha naval multiplayer onde dois jogadores se enfrentam em tempo real, posicionando frotas e disparando tiros em turnos alternados. Quem afundar toda a frota inimiga primeiro vence.

O diferencial está na experiência: uma interface inspirada nas animações Rubber Hose dos anos 1930 com estética Film Noir, efeitos de película antiga, mascotes animados e transições cinematográficas — tudo isso rodando em uma arquitetura moderna com WebSocket para comunicação instantânea.

## Como Funciona

```
┌─────────────┐     ┌─────────────────┐     ┌──────────────┐     ┌─────────────┐
│  Criar Sala │ ──▶ │ Posicionar Frota │ ──▶ │  Batalha!    │ ──▶ │  Resultado  │
│  ou Entrar  │     │   (5 navios)     │     │ (turnos 20s) │     │  + Ranking  │
└─────────────┘     └─────────────────┘     └──────────────┘     └─────────────┘
```

| Recurso | Descrição |
|---------|-----------|
| ⏱️ Turnos cronometrados | 20 segundos por jogada — hesitou, o sistema atira por você |
| 🔗 Salas por código | Compartilhe um código de 6 caracteres para jogar com amigos |
| 🏆 Ranking global | Top 20 jogadores por vitórias, com taxa de win/loss |
| 🔄 Reconexão | Caiu? Você tem 30 segundos para voltar sem perder a partida |
| 🎬 Estética cinematográfica | Grain de película, transições iris wipe, mascotes animados |

## Arquitetura

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

## Repositórios

| Repo | Descrição |
|------|-----------|
| [`navalis-api`](https://github.com/navalis-studio/navalis-api) | API REST + WebSocket STOMP, domain model DDD, autenticação JWT, testes unitários |
| [`navalis-web`](https://github.com/navalis-studio/navalis-web) | Interface do jogador, sistema de áudio, animações, reconexão automática |

## Design: Ink & Iron Noir

O visual do Navalis é uma fusão de três referências:

- **Rubber Hose (1930s)** — formas arredondadas, animações squash & stretch, mascotes com luva Mickey
- **Film Noir** — monocromia estrita, grão de película, vinheta, sombras duras
- **Brutalismo** — bordas grossas, hard shadows, tipografia bold

> Paleta: `#131313` · `#000000` · `#FFFFFF` · `#C2C2C2` · `#6E6E6E`

---

<p align="center">
  <strong>Navalis Studio</strong> · Desenvolvido por <a href="https://github.com/jhowzluk">@jhowzluk</a>
</p>
