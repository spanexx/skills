---
name: nodejs
description: Build Node.js services (BFF, integrations, workers, webhooks)
compatibility: Node.js 20+
metadata:
  domain: integrations
---

# Node.js Backend Skill

## When to use
Use this skill when you need to implement or maintain a Node.js backend service, including:
- HTTP APIs (REST)
- Webhooks
- Background workers / cron jobs
- Integrations (3rd-party APIs)
- BFF (Backend-for-Frontend)

## Core rules
- Prefer TypeScript for production services.
- Keep I/O boundaries explicit (HTTP, DB, queues, external APIs).
- Fail safely: don’t leak secrets in errors, logs, or responses.
- Avoid hidden behavior: prefer deterministic config and explicit timeouts.

## Procedure

### 1) Identify service type and entrypoint
- If the workspace uses a framework (NestJS/Express/Fastify), follow its conventions.
- Find the entrypoint and scripts in `package.json` (e.g. `start:dev`, `build`, `test`).

### 2) Define the API boundary / contracts
- For HTTP APIs:
  - Define routes, request/response shapes, error codes.
  - Prefer OpenAPI if the repo already uses it.
- For integrations:
  - Define the external endpoints, auth method, retries, and timeouts.

### 3) Environment variables
- Add a `.env.example` with all required variables.
- Do not hardcode credentials.
- Prefer a single connection variable when possible (e.g. `DATABASE_URL`, `REDIS_URL`).

### 4) Implement business logic with testable units
- Keep controllers/handlers thin.
- Put logic into service modules/functions that can be unit tested.
- For external calls:
  - Use explicit timeouts.
  - Add retry only for idempotent operations.

### 5) Error handling and status codes
- Return correct HTTP status codes.
- Use safe error messages.
- Log internal context (request id, upstream error codes), but never secrets.

### 6) Verification commands (minimum)
Run what exists in the repo; typical Node checks:

```bash
npm run lint
npm test
npm run build
```

If it’s a dev server:

```bash
npm run start:dev
```

## Acceptance checklist
- [ ] Service starts and handles requests
- [ ] Environment variables documented in `.env.example`
- [ ] Errors are safe and status codes are correct
- [ ] Build/tests/lint pass (or you documented the reason they can’t)
