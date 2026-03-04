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

Prefer official CLI setup.

ESLint (official):

```bash
npm init @eslint/config@latest
```

Prettier (official, recommended):

```bash
npm install --save-dev --save-exact prettier
```

Then create config files (official docs example):

```bash
node --eval "fs.writeFileSync('.prettierrc','{}\n')"
node --eval "fs.writeFileSync('.prettierignore','# Ignore artifacts:\nbuild\ncoverage\n')"
```

Optional integrations:
- For TypeScript projects, the ESLint init flow will offer TypeScript support and install the needed packages.
- To avoid rule conflicts, you can add `eslint-config-prettier` if you use ESLint for formatting-adjacent rules.

### 3) Configure
- Prefer minimal, non-conflicting rules
- Ensure Prettier runs last

### 4) Editor support
- Recommend VS Code settings if repo uses them

### 5) Verification

Run ESLint (example from official docs):

```bash
npx eslint .
```

Run Prettier:

```bash
npx prettier . --write
```

For CI (official):

```bash
npx prettier . --check
```

## Acceptance checklist
- [ ] Lint script exists
- [ ] Format script exists
- [ ] Config files committed
