---
name: nestjs
description: Build and maintain NestJS backend applications: modules, controllers, services, DTO validation, config, logging, auth patterns, and best practices. Use when implementing APIs with NestJS.
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["nestjs", "node", "backend", "api", "typescript"]
compatibility: Requires Node.js >= 18, TypeScript, and NestJS tooling. Internet access for package install is usually required.
license: Proprietary
---

# NestJS Skill

## When to use
- Creating NestJS modules/controllers/services
- Designing clean API boundaries (DTOs, validation)
- Adding configuration, logging, and production readiness

## Outputs
- A NestJS feature implemented with:
  - Module
  - Controller
  - Service
  - DTOs + validation
- Updated imports/wiring
- A short verification command list (build/test)

## Core rules
- Keep controllers thin; put logic in services.
- Use DTOs for request/response shapes.
- Validate inputs with `class-validator` + `class-transformer`.
- Prefer dependency injection and interfaces for boundaries.

## Procedure

### 1) Identify the feature boundary
- Define the domain object(s)
- Define API endpoints and resources

### 2) Create module structure
Typical layout:

```
src/
  modules/
    users/
      users.module.ts
      users.controller.ts
      users.service.ts
      dto/
        create-user.dto.ts
```

### 3) Add DTO validation
- Add decorators like `@IsString()`, `@IsEmail()`, etc.
- Ensure `ValidationPipe` is enabled globally.

### 4) Error handling
- Throw `HttpException` / `BadRequestException` etc.
- Keep error messages deterministic and safe.

### 5) Config + env
- Use `@nestjs/config`
- Provide `.env.example`

### 6) Testing
- Add unit tests for services where feasible.
- Add e2e tests if the repo already has that setup.

## Common pitfalls
- Putting DB logic directly into controllers
- Missing `ValidationPipe` leads to unvalidated inputs
- Leaking internal errors to clients

## Acceptance checklist
- [ ] Endpoints respond correctly
- [ ] DTO validation rejects bad inputs
- [ ] Service unit tests (if repo uses tests)
- [ ] Module is wired into the app
