---
title: Resilience4j
aliases:
  - Resilience4j
domain: Microservices
module: Resilience
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - microservices
related:
  - "[[Resilience Index|Resilience]]"
  - "[[Circuit Breaker]]"
  - "[[Retry]]"
  - "[[Bulkhead]]"
  - "[[Rate Limiting]]"
---

# Resilience4j

## Overview
Resilience4j is a lightweight, functional fault-tolerance library for Java, and the standard replacement for the deprecated Netflix Hystrix. It provides composable modules you apply per call. This note is the sub-hub for the patterns.

## Why It Matters
It's how resilience patterns are implemented in modern Spring apps — modular (use only what you need), annotation- or decorator-based, and integrated with Spring Boot + Micrometer metrics.

## Modules
| Module | Purpose | Note |
|--------|---------|------|
| CircuitBreaker | fail fast on failing deps | [[Circuit Breaker]] |
| Retry | re-attempt transient errors | [[Retry]] |
| Bulkhead | isolate concurrent calls | [[Bulkhead]] |
| RateLimiter | cap call rate | [[Rate Limiting]] |
| TimeLimiter | timeout long calls | - |

## Usage
```java
@CircuitBreaker(name = "svc", fallbackMethod = "fb")
@Retry(name = "svc")
@Bulkhead(name = "svc")
public Data call() { ... }
```
```yaml
resilience4j:
  circuitbreaker:
    instances:
      svc: { failureRateThreshold: 50, slidingWindowSize: 20, waitDurationInOpenState: 10s }
```

## Ordering Of Decorators
When combined, the typical order is: `Bulkhead -> TimeLimiter -> RateLimiter -> CircuitBreaker -> Retry` (Retry outermost so it re-runs the whole protected call). Order matters — misordering causes retries to bypass the breaker.

## Hystrix vs Resilience4j
- Hystrix: thread-pool per dependency, heavier, in maintenance.
- Resilience4j: modular, functional, lower overhead, Micrometer metrics, actively maintained.

## Interview Questions
- **What replaced Hystrix?** Resilience4j — modular and lighter.
- **Which patterns does it provide?** Circuit breaker, retry, bulkhead, rate limiter, time limiter.
- **Why does decorator order matter?** Retry should wrap the circuit breaker; wrong order lets retries hammer past an open breaker.

## Related Topics
- [[Circuit Breaker]] · [[Retry]] · [[Bulkhead]] · [[Rate Limiting]]

## Quick Revision
- Modular fault-tolerance lib (replaces Hystrix): CircuitBreaker, Retry, Bulkhead, RateLimiter, TimeLimiter. Annotation/decorator based; mind decorator order (Retry outermost).
