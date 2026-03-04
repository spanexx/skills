---
name: eslint-prettier
description: Add ESLint + Prettier to JS/TS projects with consistent rules, editor integration, and CI-ready scripts. Use when standardizing code style and catching bugs early.
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["eslint", "prettier", "lint", "format", "typescript"]
compatibility: Requires Node.js tooling.
license: Proprietary
---

# ESLint + Prettier Skill

## Outputs
- ESLint config aligned to project type (JS/TS)
- Prettier config
- Scripts:
  - `lint`
  - `format`
  - optional `lint:fix`

## Procedure

### 1) Detect stack
- Node JS
- Node TS
- NestJS (TS)

### 2) Install dependencies
- `eslint`
- `prettier`
- For TS: `@typescript-eslint/parser`, `@typescript-eslint/eslint-plugin`
- Optional: `eslint-config-prettier`

### 3) Configure
- Prefer minimal, non-conflicting rules
- Ensure Prettier runs last

### 4) Editor support
- Recommend VS Code settings if repo uses them

### 5) Verification
- `npm run lint` passes
- `npm run format -- --check` (if implemented) passes

## Acceptance checklist
- [ ] Lint script exists
- [ ] Format script exists
- [ ] Config files committed
