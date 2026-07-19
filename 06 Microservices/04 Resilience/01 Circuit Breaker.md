---
title: Circuit Breaker
aliases:
  - Circuit Breaker
domain: Microservices
module: Resilience
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - microservices
related:
  - "[[Resilience4j]]"
  - "[[Retry]]"
---

# Circuit Breaker

## Overview
A circuit breaker wraps a remote call and **stops calling** a dependency that is failing, failing fast instead of piling up requests on a dead/slow service. It borrows the electrical metaphor: trip the circuit to protect the system.

## Why It Matters
It's the key defense against **cascading failures** — without it, one slow dependency exhausts threads/connections upstream and takes down the whole chain. Top-tier interview topic.

## States
```
CLOSED  --failures exceed threshold-->  OPEN
OPEN    --after wait duration-->         HALF_OPEN
HALF_OPEN --trial calls succeed-->       CLOSED
HALF_OPEN --trial calls fail-->          OPEN
```
- **Closed** — calls flow; failures are counted.
- **Open** — calls are rejected immediately (fail fast); a **fallback** may run.
- **Half-open** — after a cooldown, a few trial calls test recovery; success closes it, failure re-opens.

## Configuration (Resilience4j)
- `failureRateThreshold` (e.g., 50%), `slidingWindowSize`, `waitDurationInOpenState`, `permittedNumberOfCallsInHalfOpenState`, `slowCallRateThreshold` (treat slow calls as failures).

## With Fallbacks
```java
@CircuitBreaker(name = "inventory", fallbackMethod = "fallback")
public Stock get(String sku) { return client.getStock(sku); }
public Stock fallback(String sku, Throwable t) { return Stock.unknown(sku); } // degrade gracefully
```

## Best Practices
- Provide a meaningful fallback (cached/default) rather than an error.
- Combine with timeouts (a slow call is a failure) and [[Bulkhead]] isolation.
- Don't blindly [[Retry]] through an open breaker.

## Interview Questions
- **Circuit breaker states?** Closed -> Open -> Half-Open, based on failure/slow-call rate and a cooldown.
- **What problem does it solve?** Cascading failures — it fails fast instead of hammering a broken dependency.
- **How is half-open used?** Sends limited trial calls to test recovery before fully closing.

## Related Topics
- [[Resilience4j]] · [[Retry]] · [[Bulkhead]] · [[Synchronous vs Asynchronous Communication]]

## Quick Revision
- Fail fast on a failing dependency. Closed->Open->Half-Open by failure/slow-call rate + cooldown. Add fallback + timeout; prevents cascading failures.
