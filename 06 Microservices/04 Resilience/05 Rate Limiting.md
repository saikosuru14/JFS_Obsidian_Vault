---
title: Rate Limiting
aliases:
  - Rate Limiting
domain: Microservices
module: Resilience
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 5
tags:
  - microservices
related:
  - "[[Resilience4j]]"
---

# Rate Limiting

## Overview
Rate limiting caps how many requests a client or service may make in a time window, protecting backends from overload and abuse and enforcing fair usage/quotas.

## Why It Matters
It's both a resilience control (shed load before you fall over) and a business/security control (per-tenant quotas, anti-abuse). Knowing the algorithms and where to enforce it is expected.

## Algorithms
| Algorithm | Idea | Notes |
|-----------|------|-------|
| **Token bucket** | tokens refill at a rate; each request spends one | allows bursts up to bucket size (most common) |
| **Leaky bucket** | requests drain at a fixed rate | smooths bursts into a steady flow |
| **Fixed window** | count per fixed interval | simple; boundary spikes |
| **Sliding window** | rolling count | smoother, more accurate |

## Where To Enforce
- **API Gateway** — global/edge limits per client/IP/API key ([[Spring Cloud Gateway]] `RequestRateLimiter` + Redis).
- **Per service** — Resilience4j `RateLimiter` for internal protection.

## Responses
- Return **HTTP 429 Too Many Requests** with a `Retry-After` header.
- For distributed limits, keep counters in a shared store (Redis) so all instances share the budget.

## Interview Questions
- **Token vs leaky bucket?** Token bucket permits bursts (spend accumulated tokens); leaky bucket enforces a steady drain rate.
- **Where do you rate limit?** At the gateway for client-facing limits; per service for internal protection.
- **How for a cluster?** Centralize counters (e.g., Redis) so the limit is global, not per instance.

## Related Topics
- [[API Gateway]] · [[Bulkhead]] · [[Resilience4j]]

## Quick Revision
- Cap request rate to protect + enforce quotas. Token bucket (bursty) / leaky (smooth) / fixed / sliding window. Enforce at gateway (Redis) or per service (Resilience4j); return 429.
