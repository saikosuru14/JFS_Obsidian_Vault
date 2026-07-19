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

> Fast recall for [[System Design]]. See the [[System Design Index|domain]] for depth.

## Interview Flow
1. Clarify functional + non-functional requirements.
2. Capacity estimation (QPS, storage, bandwidth).
3. API design → high-level architecture → data model.
4. Deep-dive a component; discuss bottlenecks and trade-offs.

## Scaling
- Vertical (bigger box) vs horizontal (more boxes + load balancer).
- Stateless services scale easily; externalize state (cache/DB/session store).

## Building Blocks
- Load balancer (L4/L7), reverse proxy, CDN (edge caching), message queue (async decoupling).
- Cache strategies: cache-aside, write-through, write-back; eviction: LRU/LFU/TTL.

## Data
- Replication (read scaling, HA) vs sharding/partitioning (write scaling).
- Consistent hashing to minimize resharding.
- **CAP:** on partition, choose consistency (CP) or availability (AP).
- SQL (ACID, joins) vs NoSQL (scale, flexible schema); pick per access pattern.

## Reliability
- Redundancy, health checks, retries + backoff, circuit breakers, idempotency.
- Rate limiting (token bucket) to protect services.

## Numbers to Know
- Memory ns, SSD µs, network ms; 1 day ≈ 86,400 s.

## Top Interview One-Liners
- Latency vs throughput: per-request time vs work per unit time.
- How to scale writes? Shard/partition.
- Ensure idempotency? Idempotency keys + dedup.

## Revision Checklist
- [ ] Requirements + capacity estimation
- [ ] Horizontal scaling + statelessness
- [ ] Caching + CDN + queues
- [ ] Replication vs sharding; CAP
- [ ] Reliability patterns
