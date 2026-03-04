---
name: nodejs-init
description: Initialize a Node.js project from scratch or standardize an existing one (package.json, TypeScript optional, linting, scripts, env, and folder structure). Use when setting up Node services, CLIs, scripts, or backend APIs.
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["node", "npm", "project-setup", "typescript", "tooling"]
compatibility: Requires Node.js >= 18 and a package manager (npm/pnpm/yarn). Requires filesystem access.
license: Proprietary
---

# Node.js Project Initialization Skill

## When to use
- Starting a new Node.js project
- Cleaning up / standardizing an existing Node repo
- Adding baseline scripts, conventions, and tooling

## Outputs
- A working `package.json` with:
  - `name`, `version`, `private` (if app)
  - scripts for `dev`, `build` (if TS), `test` (if present), `lint` (if present)
- A reasonable folder structure
- `.gitignore` and `.env.example`

## Procedure

### 1) Decide project mode
Choose one:
- **JavaScript** (fastest)
- **TypeScript** (recommended for services)

### 2) Initialize package manager metadata
- Ensure `package.json` exists.
- Add scripts aligned to the chosen build tool.

Recommended scripts (TS + Node):
- `dev`: run with watch (e.g. `tsx watch src/index.ts`)
- `build`: `tsc -p tsconfig.json`
- `start`: `node dist/index.js`

### 3) Pick runtime + tooling
Recommended baseline:
- Node.js 18+
- `dotenv` for env (or framework-specific)
- `pino` for structured logging (optional)

### 4) Environment setup
- Create `.env.example` with required variables.
- Ensure `.env` is gitignored.

### 5) Folder structure
Recommended service layout:

```
.
├── src/
│   ├── index.ts
│   └── ...
├── test/ (optional)
├── package.json
└── README.md
```

### 6) Verification
- `npm run dev` starts successfully
- A basic entrypoint prints a startup message

## Common pitfalls
- Mixed ESM/CJS configuration without clarity
- Missing `type: module` when using ESM
- Missing Node version constraints

## Acceptance checklist
- [ ] `package.json` exists and scripts run
- [ ] `src/index.*` exists and executes
- [ ] `.env.example` exists
- [ ] `.gitignore` ignores `node_modules`, `dist`, and `.env`
