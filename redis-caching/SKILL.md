---
name: redis-caching
description: "Implement caching with Redis in Node/NestJS: cache-aside, TTL strategy, invalidation, key design, and safety. Use when improving performance with Redis caching."
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

## NestJS: official cache module (current)

### 1) Install

For NestJS caching, install the official packages:

```bash
npm install @nestjs/cache-manager cache-manager
```

If you run into npm peer dependency conflicts in an existing repo, retry with:

```bash
npm install @nestjs/cache-manager cache-manager --legacy-peer-deps
```

### 2) Enable CacheModule

In your module (often `AppModule`), enable caching:

```ts
import { CacheModule } from '@nestjs/cache-manager';

imports: [CacheModule.register()],
```

Common options:

```ts
CacheModule.register({
  isGlobal: true,
  ttl: 5000, // milliseconds
});
```

### 3) Use the cache manager

Inject using the `CACHE_MANAGER` token:

```ts
import { CACHE_MANAGER, Cache } from '@nestjs/cache-manager';

constructor(@Inject(CACHE_MANAGER) private cacheManager: Cache) {}
```

Then:

```ts
await this.cacheManager.get('key');
await this.cacheManager.set('key', 'value', 1000);
await this.cacheManager.del('key');
await this.cacheManager.clear();
```

### 4) Switch to Redis store (Keyv)

Nest's cache-manager uses Keyv underneath; to use Redis install:

```bash
npm install @keyv/redis
```

If you run into peer-deps conflicts in an existing repo, this combination worked in practice:

```bash
npm install @nestjs/cache-manager cache-manager @keyv/redis --legacy-peer-deps
```

Then register a Redis store (example pattern uses `registerAsync`):

```ts
import KeyvRedis from '@keyv/redis';

CacheModule.registerAsync({
  useFactory: async () => ({
    stores: [new KeyvRedis(process.env.REDIS_URL ?? 'redis://localhost:6379')],
  }),
});
```

#### Real-world dev note: port conflicts

If you already have Redis on `6379`, map Docker Redis to a different host port (example: `6380`) and set:

```bash
REDIS_URL=redis://localhost:6380
```

When verifying cache behavior, consider returning an `X-Cache: MISS|HIT` header and logging `CACHE_MISS`/`CACHE_HIT` to prove the second request is served from cache.

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
