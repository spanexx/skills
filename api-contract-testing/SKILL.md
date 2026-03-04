---
name: api-contract-testing
description: Validate API request/response contracts and compatibility across services
compatibility: Contract testing (OpenAPI-based)
metadata:
  domain: testing
---

# API Contract Testing Skill

## When to use
Use this skill when you need to:
- Prevent breaking API changes
- Validate that implementation matches the OpenAPI contract
- Validate clients/consumers still work after changes
- Add CI checks for API compatibility

## Preferred contract source
- If the backend is code-first (NestJS Swagger), the generated OpenAPI document is the contract artifact.
- If the repo is spec-first, the OpenAPI YAML/JSON is the contract artifact.

## Procedure

### 1) Identify producers and consumers
- **Producer**: the API service.
- **Consumer(s)**: frontend app, other services, QA scripts.

### 2) Define “contract” scope
Minimum contract coverage:
- Path + method
- Required params
- Request body schema
- Success response schema
- Error response shape

### 3) Test strategies (choose what fits the repo)
- **Schema validation tests**:
  - Call endpoints and validate responses against OpenAPI.
- **Snapshot the OpenAPI doc**:
  - Commit a generated `openapi.json` and diff changes in PRs.
- **Consumer-driven checks**:
  - Use frontend expectations as a “consumer contract” (lightweight).

### 4) Add CI-friendly commands
Ensure the repo has deterministic scripts:
- Build backend
- Run tests
- (Optional) Generate spec artifact and compare

### 5) Verification
Run what exists. Typical NestJS backend:

```bash
npm test
npm run build
```

If you add an artifact diff step, ensure it fails with a clear message when the contract changed.

## Acceptance checklist
- [ ] Contract checks fail on breaking changes
- [ ] Error responses are part of the contract
- [ ] Tests run deterministically in CI
