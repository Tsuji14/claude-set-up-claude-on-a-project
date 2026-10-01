# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

A minimal Express REST API used as the base project for a Claude Code course. Endpoints: `GET/POST /users` and `GET /health`.

## Commands

```bash
npm install        # install dependencies
npm run dev        # start API with file-watching on http://localhost:3000
npm test           # run all tests (Node built-in test runner)
npm run lint       # ESLint check
```

To run a single test file: `node --test tests/users.test.js`

## Architecture

- `server.js` — creates the Express app, mounts routes, and exports `app` (does not call `listen` when imported, so tests work without opening a port)
- `routes/` — one file per resource (`users.js`, `health.js`); each exports an Express Router
- `db/store.js` — in-memory data layer; all data access goes through its exported functions (`getAllUsers`, `getUserById`, `createUser`); data resets on restart

## Conventions

- Use CommonJS (`require`/`module.exports`), not ES modules — `package.json` has no `"type": "module"`
- Route handlers validate input and return structured JSON errors (`{ error: "..." }`) with appropriate HTTP status codes
- `PORT` is read from `process.env.PORT`; real config belongs in `.env` (git-ignored), never committed
