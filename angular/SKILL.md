---
name: angular
description: "Build and maintain Angular frontend applications: components, routing, services, forms, state, and testing. Use when implementing Angular features in a fullstack app."
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["angular", "frontend", "typescript", "spa"]
compatibility: Requires Node.js and Angular CLI. Works with Angular 17+ (adapt to repo version).
---

# Angular Skill

## When to use
Use this skill when you need to:
- Implement screens and components in Angular
- Add routes, guards, and layouts
- Build forms (reactive forms) with validation
- Call backend APIs via `HttpClient`
- Add UI patterns (loading/error/empty states)

## Core rules
- Keep components focused; push business logic into services.
- Prefer standalone components if the repo uses them.
- Use reactive forms for non-trivial forms.
- Always implement real behaviors for interactive UI elements (no dead buttons/links).

## Procedure

### 1) Identify project conventions
- Check Angular version and whether the repo uses:
  - standalone components
  - NgModules
  - Tailwind or other styling
  - Vitest/Karma/Jasmine
- Find existing patterns for:
  - API services
  - routing
  - layout

### 2) Plan the feature
- Define the UI states:
  - loading
  - error
  - empty
  - success
- Define the data contract with the backend.

### 3) Generate scaffolding (preferred)
Use Angular CLI where appropriate:

```bash
ng generate component <name>
ng generate service <name>
```

If routing changes are needed, update the router config and ensure links navigate to real routes.

### 4) Data access
- Create an API service that:
  - has a single responsibility (e.g. `UsersApi`)
  - uses typed DTOs/interfaces
  - handles errors deterministically
- Avoid duplicating base URLs; centralize API base config.

### 5) Forms
- Use `FormGroup` + validators.
- Show validation errors only after user interaction (touched/dirty) or submit.

### 6) Verification
Run the repo’s existing commands. Typical:

```bash
npm run build
npm test
npm run start
```

## Acceptance checklist
- [ ] Routes and links work (no dead navigation)
- [ ] Loading/error/empty states exist
- [ ] Components are typed and template errors are resolved
- [ ] Build and tests pass
