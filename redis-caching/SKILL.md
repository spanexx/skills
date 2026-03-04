---
name: redis-caching
description: Implement caching with Redis in Node/NestJS: cache-aside, TTL strategy, invalidation, key design, and safety. Use when improving performance with Redis caching.
metadata:
  author: spanexx
  version: "1.0.0"
  tags: ["redis", "caching", "performance", "nestjs", "node"]
compatibility: Requires Redis access (local Docker or managed Redis) and Node.js. Network access to Redis required.
license: Proprietary
---

# Redis Caching Skill

## When to use
- Adding Redis cache to reduce DB/API load
- Designing cache keys + TTLs
- Adding invalidation on writes

## Outputs
- Cache strategy documented (cache-aside / write-through)
- Implementation in code with:
  - key design
  - TTL selection
  - invalidation plan
- Verification steps (how to confirm cache hits)

## Recommended approach: Cache-aside
### Read path
1. Compute cache key
2. `GET` from Redis
3. If hit: return
4. If miss: read from source, `SET` with TTL, return

### Write path
- After successful write to source:
  - delete/expire affected keys
  - or update cached value

## Key design
- Use stable prefixes:
  - `user:<id>`
  - `project:<id>`
  - `list:projects:<filters-hash>`
- Keep keys short and deterministic.

## TTL strategy
- Default TTL for read models: 60s to 10m depending on staleness tolerance
- Avoid caching highly volatile data unless you can invalidate correctly

## Invalidation
- Prefer targeted `DEL` for entity keys
- For list caches, consider:
  - shorter TTL
  - versioned keys (e.g. `list:projects:v3:<hash>`)

## Failure modes
- Redis down: system should degrade gracefully (bypass cache)
- Cache stampede: consider request coalescing / locking for hot keys

## Security
- Never cache secrets
- Sanitize user input used in keys (hash it)

## Acceptance checklist
- [ ] Cache hits are observable (logs/metrics)
- [ ] TTLs are set intentionally
- [ ] Writes invalidate/update cache
- [ ] Redis outage does not take the app down
