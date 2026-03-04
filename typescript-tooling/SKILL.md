---
name: typescript-tooling
description: Add or standardize TypeScript tooling in a Node project (tsconfig, build, path aliases, strictness, and runtime execution). Use when migrating JS to TS or setting up TS from scratch.
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["typescript", "node", "tooling", "build"]
compatibility: Requires Node.js and a package manager.
license: Proprietary
---

# TypeScript Tooling Skill

## Outputs
- `tsconfig.json` aligned to project type
- Build + dev scripts (and runtime choice)
- Clear module system choice: ESM or CJS

## Procedure

### 1) Choose module system
- Prefer ESM for modern projects
- Ensure consistency across `package.json`, tsconfig, and runtime

### 2) Add dependencies
- `typescript`
- Optional runtime: `tsx` (fast dev)

### 3) Create/adjust tsconfig
- Recommended:
  - `strict: true`
  - `noUncheckedIndexedAccess: true` when feasible
  - `outDir: dist`

### 4) Scripts
- `dev`: `tsx watch src/index.ts`
- `build`: `tsc -p tsconfig.json`
- `start`: `node dist/index.js`

### 5) Verification
- `npm run build` succeeds
- `npm run dev` runs

## Acceptance checklist
- [ ] Type checking is enabled
- [ ] Dev and build scripts are consistent
- [ ] Output is emitted to `dist/`
