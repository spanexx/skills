---
name: docker-dev
description: Add Docker and docker-compose for local development (services like Redis/Postgres), including environment variables and developer workflow. Use when you need reproducible dev environments.
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["docker", "compose", "dev-env", "redis", "postgres"]
compatibility: Requires Docker engine and docker compose.
license: Proprietary
---

# Docker Dev Environment Skill

## Outputs
- `docker-compose.yml` (or `compose.yaml`)
- `.env.example` for service ports/passwords
- Documentation of how to start/stop

## Procedure

### 1) Identify services
Common:
- Redis
- Postgres
- Mongo

### 2) Compose file
- Use named volumes
- Expose ports
- Provide healthchecks where helpful

### 3) App integration
- Ensure app reads env vars for connection
- Avoid hardcoding localhost/ports

### 4) Verification
- `docker compose up -d`
- Connect from app and confirm

## Acceptance checklist
- [ ] `docker compose up` works from clean checkout
- [ ] `.env.example` includes required vars
- [ ] Volumes persist data
