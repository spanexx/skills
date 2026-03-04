---
name: qa-engineer
description: "Improve quality for fullstack apps (NestJS + Angular): test planning, test cases, automation hooks, and regression safety. Use when adding tests or validating behavior changes."
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["qa", "testing", "nestjs", "angular", "e2e", "regression"]
compatibility: Works with Node.js tooling. Uses whatever test runner the repo already has (Jest/Vitest/Playwright/Cypress).
---

# QA Engineer Skill

## When to use
Use this skill when you need to:
- Turn a feature into a test plan
- Create manual test cases for a PR
- Add automated tests (unit/integration/e2e)
- Validate API contracts and UI flows

## Core rules
- Prefer small, deterministic tests over flaky end-to-end tests.
- Never depend on external networks in unit tests.
- Every bug fix should come with a regression test when feasible.

## Procedure

### 1) Clarify the scope
- What changed?
- Who is impacted?
- What are the success criteria?

### 2) Produce a test plan
For each feature/bug:
- Happy path
- Validation / bad inputs
- Auth/permission boundaries (if applicable)
- Error handling
- Performance-sensitive paths (if applicable)

### 3) Decide test levels
- Backend unit tests (service logic)
- Backend integration tests (controller + pipes + validation)
- Frontend component tests (render + interaction)
- Frontend integration tests (routing + API mocking)
- E2E tests (critical flows only)

### 4) Add automation using repo tooling
- Backend (NestJS): Jest + `@nestjs/testing`
- Frontend (Angular): use the repo’s existing runner (often `ng test`)

### 5) Verification
Run existing scripts:

```bash
# Backend
npm test

# Frontend
npm test
```

## Acceptance checklist
- [ ] Test plan covers happy path + key edge cases
- [ ] At least one automated test added for meaningful changes (when feasible)
- [ ] Tests are deterministic and CI-friendly
