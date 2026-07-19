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
order: 8
tags:
  - revision
  - system-design
---

# System Design Cheat Sheet

> Mid-level recall for [[System Design]] — the framework, numbers, and trade-offs.

## Interview Framework
1. Clarify **functional + non-functional** requirements (scale, latency SLO, consistency).
2. **Capacity estimate**: DAU → QPS (peak ≈ 2–3× avg), storage/day, bandwidth.
3. API + data model → high-level architecture → deep-dive one component → bottlenecks/trade-offs.

## Numbers to Know
- L1 ~1 ns, main memory ~100 ns, SSD read ~100 µs, network round trip within DC ~0.5 ms, cross-region ~50–150 ms.
- 1 day ≈ 86,400 s; 1M/day ≈ 12 QPS avg. Read:write ratio drives caching/replication.

## Scaling
- Vertical (limits) vs horizontal (+ load balancer). Make services **stateless** (externalize sessions to Redis/DB) so they scale flat.
- LB: L4 (fast, TCP) vs L7 (routing/TLS). CDN for static + edge caching.

## Caching
- Patterns: **cache-aside** (lazy, most common), write-through, write-back. Eviction: LRU/LFU/TTL.
- Invalidation is the hard part; watch thundering herd (use locks/request coalescing), stampede, hot keys.

## Data
- **Replication** (read scaling, HA) vs **sharding/partitioning** (write scaling; pick a shard key that avoids hot spots; **consistent hashing** to minimize resharding).
- **CAP**: on partition choose C or A. **PACELC**: else, latency vs consistency.
- SQL (ACID, joins) vs NoSQL (scale, denormalized, per-access-pattern). Consistency: strong vs eventual vs read-your-writes.

## Reliability & Async
- Redundancy, health checks, **retries with backoff + jitter**, **circuit breakers**, **idempotency keys** (dedupe on retries), bulkheads, timeouts.
- **Rate limiting**: token bucket (bursts) / leaky bucket / sliding window; enforce at gateway (Redis).
- Message queues (SQS/Kafka) to decouple, smooth spikes, and enable retries/DLQ. Outbox pattern for reliable event publishing.

## Case-Study Reflexes
- URL shortener → base62 + KGS/counter; feed → fan-out on write vs read; chat → WebSockets + presence; payments → idempotency + saga.

## Sharp Interview Answers
- Drive requirements + estimation *first*.
- How to scale writes (shard) vs reads (replicas/cache).
- Ensure idempotency; prevent cache stampede; pick a shard key.
- CAP/PACELC trade-off for the chosen store.

## Revision Checklist
- [ ] Framework + capacity estimation + latency numbers
- [ ] Stateless scaling + LB (L4/L7) + CDN
- [ ] Caching patterns + invalidation pitfalls
- [ ] Replication vs sharding + consistent hashing + CAP/PACELC
- [ ] Retries/backoff, circuit breaker, idempotency, rate limiting, queues
