---
title: System Design Cheat Sheet
aliases:
  - System Design Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 9
tags:
  - revision
  - system-design
---

# System Design Cheat Sheet

> Interview-ready revision for [[System Design]] (4–5 YOE). Framework, numbers, trade-offs, and Q&A with answers.

---

## 1. Interview Framework (drive it in this order)
1. **Requirements** — functional (features) + non-functional (scale, latency SLO, availability, consistency). Clarify read:write ratio.
2. **Capacity estimate** — DAU → QPS (peak ≈ 2–3× avg), storage/day, bandwidth, cache size.
3. **API** (endpoints/contracts) → **high-level architecture** (client → LB → services → cache/DB/queue) → **data model**.
4. **Deep dive** one component; discuss **bottlenecks & trade-offs**; then reliability/observability.

## 2. Numbers to Know
- L1 ~1 ns, RAM ~100 ns, SSD read ~100 µs, DC round-trip ~0.5 ms, cross-region ~50–150 ms.
- 1 day ≈ 86,400 s → 1M req/day ≈ 12 QPS avg. Estimate storage = records × size × retention × replication.

## 3. Building Blocks
- **Load balancer**: L4 (TCP, fast) vs L7 (HTTP routing, TLS). Health checks + sticky sessions (avoid — externalize state).
- **Cache** (Redis): read-through / cache-aside; sits in front of DB.
- **CDN**: static/edge caching close to users.
- **Message queue** (SQS/Kafka): decouple, absorb spikes, retries, async work.
- **Reverse proxy / API gateway**: routing, auth, rate limiting, TLS.

## 4. Scaling
- Vertical (simple, limited) vs **horizontal** (+ LB, the real answer). Make services **stateless** → externalize sessions to Redis/DB so any instance serves any request.
- Split reads (replicas/cache) from writes; async the non-critical path via queues.

## 5. Caching (and its traps)
| Pattern | How |
|---------|-----|
| Cache-aside | app reads cache, on miss loads DB + populates (most common) |
| Read-through | cache library loads on miss |
| Write-through | write cache + DB synchronously |
| Write-back | write cache, async to DB (fast, risk on crash) |
Eviction: LRU/LFU/TTL. **Pitfalls:** stampede/thundering herd (use locks/request coalescing + jitter TTLs), hot keys, stale data (invalidation is the hard part).

## 6. Data: Replication, Sharding, Consistency
- **Replication**: read scaling + HA (leader-follower; failover). Sync (durable, slower) vs async (fast, replica lag).
- **Sharding/partitioning**: write scaling; pick a shard key with even distribution (avoid hot shards). **Consistent hashing** minimizes reshuffling when nodes change.
- **CAP**: under a network partition choose Consistency **or** Availability. **PACELC**: else, trade Latency vs Consistency.
- **Consistency models**: strong, eventual, read-your-writes, monotonic reads. Pick per feature (payments = strong; feed = eventual).
- SQL (ACID, joins, ad-hoc) vs NoSQL (scale, denormalized to access pattern). Match store to access pattern.

## 7. Reliability & Async
- Redundancy across AZs, health checks, **retries with exponential backoff + jitter** (idempotent ops only), **circuit breakers**, **timeouts**, **bulkheads**.
- **Idempotency keys** to dedupe retried writes (payments, order creation).
- **Rate limiting**: token bucket (allows bursts), leaky bucket, sliding window — enforce at gateway (Redis counters).
- **Outbox pattern** for reliable event publishing; DLQ for poison messages.

## 8. Case-Study Reflexes
- **URL shortener** → base62 of an ID (counter/KGS); read-heavy → cache + CDN.
- **News feed** → fan-out on write (precompute) vs fan-out on read (celebrities); hybrid.
- **Chat** → WebSockets + presence + message store (sharded by conversation).
- **Rate limiter** → Redis token bucket.
- **Payments** → idempotency + saga + strong consistency + audit log.

---

## 9. Interview Q&A (with answers)

**Q: How do you start a system design question?**
A: Clarify functional + non-functional requirements and the read:write ratio, do a quick capacity estimate (QPS/storage), then sketch APIs and a high-level architecture before deep-diving. Never jump to a diagram first.

**Q: How do you scale writes vs reads?**
A: Reads: replicas + caching + CDN. Writes: shard/partition by a good key, batch, and push non-critical work to async queues. Keep services stateless so they scale horizontally.

**Q: Explain CAP (and PACELC).**
A: During a partition you must choose consistency or availability. PACELC adds: even without partitions, you trade latency vs consistency. E.g., DynamoDB (AP/low-latency, tunable) vs a strongly consistent RDBMS (CP).

**Q: How do you prevent a cache stampede?**
A: Add jitter to TTLs, use a lock / request coalescing so only one loader repopulates a hot key, and optionally serve stale-while-revalidate.

**Q: How do you guarantee a write isn't processed twice?**
A: Idempotency keys — the client sends a unique key; the server records processed keys and returns the prior result on retries. Combine with at-least-once delivery + dedupe.

**Q: How do you pick a shard key?**
A: One that distributes load evenly and matches query patterns (so most queries hit one shard). Avoid monotonic keys (hot shard) and low-cardinality keys; consistent hashing eases rebalancing.

**Q: Strong vs eventual consistency — when each?**
A: Strong for money/inventory/auth (correctness over latency). Eventual for feeds, counts, search indexes (availability/latency over immediate correctness), ideally with read-your-writes for the user's own actions.

**Q: How do you make a service resilient to a slow dependency?**
A: Timeouts + retries with backoff/jitter + circuit breaker + bulkhead + a fallback, so one failing dependency can't exhaust threads or cascade.

---

## Revision Checklist
- [ ] Framework: requirements → estimation → API → architecture → deep dive
- [ ] Latency numbers + capacity math
- [ ] LB (L4/L7), cache, CDN, queue, gateway
- [ ] Stateless horizontal scaling
- [ ] Caching patterns + stampede/invalidation
- [ ] Replication vs sharding + consistent hashing + CAP/PACELC + consistency models
- [ ] Retries/backoff, circuit breaker, idempotency, rate limiting, outbox
- [ ] Case-study reflexes
