---
name: typescript
description: Design and maintain TypeScript types, interfaces, and safe refactors
compatibility: TypeScript 5+
metadata:
  domain: types
---

# TypeScript Skill

## When to use
Use this skill when you need to:
- Add or improve type safety
- Refactor code safely (rename, extract, split modules)
- Design DTOs, API contracts, and shared types
- Fix TypeScript errors without weakening types

## Core rules
- Prefer narrowing over casting.
- Avoid `any`. If unavoidable, isolate it and document why.
- Keep types close to their domain boundary (DTOs near controllers, models near persistence, etc.).
- Use runtime validation for untrusted inputs (HTTP payloads, env vars, external API responses).

## Procedure

### 1) Identify the boundary
- Determine whether the type is for:
  - external input (request body, query params)
  - internal domain model
  - persistence model
  - external API client response

### 2) Choose the right construct
- Use `type` for unions/intersections and simple shapes.
- Use `interface` when you expect extension/merging.
- Use `enum` sparingly; consider string unions for flexibility.

### 3) Model validation vs typing
- TypeScript types do not validate at runtime.
- For NestJS DTOs, prefer `class-validator` decorators.
- For Node libraries/clients, consider schema validation patterns already present in the repo.

### 4) Make refactors safe
- Prefer IDE/TS server rename across the project.
- When splitting files:
  - keep exports stable
  - avoid circular imports
- If you change public types, update call sites and tests.

### 5) Verification
Run the repo’s checks. Typical:

```bash
npm test
npm run build
```

If the repo has linting:

```bash
npm run lint
```

## Acceptance checklist
- [ ] No new TypeScript errors introduced
- [ ] Types are not weakened to “make it compile”
- [ ] Runtime validation exists for untrusted inputs
- [ ] Build/tests/lint pass (or you documented why they can’t)
