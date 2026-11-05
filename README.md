# blocra-backend-legacy

> **Archived. Not maintained. Do not deploy.**
>
> This is BlocRA's original API, built with Node.js, Express and MongoDB. It has been replaced by
> **[blocra-backend](https://github.com/Blocra-HQ/blocra-backend)**, written in Rust with Actix-web and
> SQLite. The code is kept here for reference and for its history. Nothing in BlocRA uses it any more.

## What it contained

An Express 5 app (`server.js` → `src/app.js`) backed by MongoDB through Mongoose, with Socket.IO for
real-time updates.

| Area | Path | Contents |
|------|------|----------|
| Routes | `src/routes/` | `auth`, `bounties`, `admin`, `contracts`, `dashboards`, `queries`, all mounted under `/api` |
| Controllers | `src/controllers/` | Auth (email/password, Google, GitHub, token refresh, profile), bounties, stats |
| Models | `src/models/` | `User`, `Bounty`, `BountyParticipant`, `Submission`, `Reward`, `ContractQuery` |
| Middleware | `src/middlewares/` | JWT auth, request validation, uploads (multer), errors, WebSocket rate limiting |
| Services | `src/services/WebSocketService.js` | Socket.IO broadcasts |
| Utilities | `src/utils/` | JWT generation, Google/GitHub/Twitter OAuth helpers, logging (winston), rate limiting, env validation |

Its main endpoints were:

- **Auth:** `POST /api/auth/register`, `/login`, `/google`, `/github` and `/refresh`, plus profile and
  password routes.
- **Bounties:** create, join, submit and select a winner. This feature has since been removed from
  BlocRA.
- **Queries:** `POST /api/queries/execute` plus saving, listing and searching queries.
- **Admin:** user management and bounty moderation.

## How it ran

```bash
npm install
MONGO_URI=mongodb://localhost:27017/blocra JWT_SECRET=... npm start   # or npm run dev (nodemon)
```

The server listened on `PORT` (default 5000) once it had connected to MongoDB.

## State of the code

- **Docker:** the `Dockerfile` is empty, so no container image can be built from this repo.
- **CI:** no workflow builds or tests this code.
- **Leftovers:** a few work-in-progress files remain (`src/app.js.tmp`, `*.append.js`,
  an empty `googleAuthController.js`).
- **Tests:** there are none; `npm test` exits with an error.

For anything current, see [blocra-backend](https://github.com/Blocra-HQ/blocra-backend) and the
[organisation overview](https://github.com/Blocra-HQ).
