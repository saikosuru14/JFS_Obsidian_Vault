---
title: Bulkhead
aliases:
  - Bulkhead
domain: Microservices
module: Resilience
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 4
tags:
  - microservices
related:
  - "[[Resilience4j]]"
---

# Bulkhead

## Overview
The bulkhead pattern isolates resources (threads, connections, concurrent calls) per dependency so that one slow/failing dependency can't exhaust the shared pool and take down everything. Named after ship compartments that contain flooding.

## Why It Matters
Without isolation, a single slow downstream call can consume all worker threads, starving unrelated requests — a stealthy cause of total outages. Bulkheads contain the blast radius.

## Types (Resilience4j)
- **Semaphore bulkhead** — caps the number of **concurrent** calls (lightweight, default).
- **Thread-pool bulkhead** — runs calls in a **dedicated pool** with its own queue, isolating them from the caller's threads.

## Example
```yaml
resilience4j:
  bulkhead:
    instances:
      inventory: { maxConcurrentCalls: 20, maxWaitDuration: 10ms }
```

## Best Practices
- Give each critical dependency its own bulkhead so they fail independently.
- Combine with [[Circuit Breaker]] (isolate + fail fast) and [[Rate Limiting]].
- Size limits from measured concurrency, not guesses.

## Interview Questions
- **What does a bulkhead do?** Isolates resource pools per dependency so one failure can't exhaust everything.
- **Semaphore vs thread-pool bulkhead?** Cap concurrent calls in-thread vs run in a separate pool/queue.
- **How does it relate to circuit breaker?** Bulkhead isolates resources; breaker stops calls — used together for containment.

## Related Topics
- [[Circuit Breaker]] · [[Rate Limiting]] · [[Resilience4j]]

## Quick Revision
- Isolate per-dependency resources so one slow dep can't drain the shared pool. Semaphore (concurrent cap) vs thread-pool (separate pool). Combine with breaker + rate limit.
