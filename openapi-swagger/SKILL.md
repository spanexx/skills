---
name: openapi-swagger
description: Define and maintain OpenAPI specs; generate docs and clients
compatibility: OpenAPI 3.0+
metadata:
  domain: api
---

# OpenAPI + Swagger Skill

## When to use
Use this skill when you need to:
- Add/maintain OpenAPI documentation for an API
- Ensure request/response schemas are accurate
- Keep API changes compatible (versioning)
- Generate or validate clients/servers from a spec

## NestJS (common path)
If the backend is NestJS, prefer the official Swagger integration.

## Procedure

### 1) Decide source of truth
Pick one approach and stick to it in the repo:
- Code-first (NestJS decorators generate the spec)
- Spec-first (OpenAPI YAML/JSON drives implementation)

### 2) For NestJS: enable Swagger docs
Typical steps (adapt to repo conventions):
- Install `@nestjs/swagger` and `swagger-ui-express` if not already installed.
- In `main.ts`, create a Swagger document and serve it under a stable path (e.g. `/docs`).
- Use DTOs + decorators so schemas are correct.

### 3) Document auth, errors, and pagination
- Auth:
  - Document bearer auth if you use JWT.
- Errors:
  - Document error response shapes (status + message + code).
- Pagination:
  - Standardize query params (`page`, `limit`, `cursor`) and response shape.

### 4) Spec hygiene
- Keep operation ids stable.
- Keep schema names deterministic.
- Don’t leak internal fields.
- Version breaking changes (new path prefix like `/v2` or explicit version headers).

### 5) Verification
- Run backend build/tests.
- Start the server and load Swagger UI.

Typical:

```bash
npm run build
npm test
npm run start:dev
```

## Acceptance checklist
- [ ] `/docs` (or repo’s chosen path) loads
- [ ] Endpoints, schemas, and status codes are accurate
- [ ] Auth and errors are documented
- [ ] API changes are versioned when breaking
