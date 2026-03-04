---
name: jest-testing
description: "Add or extend Jest testing for Node/NestJS projects: unit tests, mocks, coverage, and CI integration. Use when setting up automated tests or improving test suites."
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["jest", "testing", "node", "nestjs", "quality"]
compatibility: Requires Node.js tooling.
license: Proprietary
---

# Jest Testing Skill

## Outputs
- Jest config (or framework-native config)
- Test scripts
- At least one representative test example (if adding new tests)

## Procedure

### 1) Detect framework
- For NestJS, prefer `@nestjs/testing` patterns.

### 2) Install dependencies

Base install:

```bash
npm install --save-dev jest
```

TypeScript options (official docs):

Option A (recommended for TS projects): `ts-jest`

```bash
npm install --save-dev ts-jest
```

Option B (Babel transpilation):

```bash
npm install --save-dev @babel/preset-typescript
```

Type definitions (pick one):

Option 1 (explicit imports):

```bash
npm install --save-dev @jest/globals
```

Option 2 (global types):

```bash
npm install --save-dev @types/jest
```

### 3) Add scripts
- `test`
- `test:watch`
- `test:cov`

### 4) Write tests
- Unit tests for service-level logic
- Mock external IO (db, http)

### 5) Verification
- `npm test`
- Coverage report generated

If you use `ts-jest`, ensure Jest is configured to transpile TS (ts-jest may require a config file depending on the repo).

## Acceptance checklist
- [ ] Tests run in CI-friendly way
- [ ] No network calls in unit tests
- [ ] Coverage command works
