---
title: Synchronous vs Asynchronous Communication
aliases:
  - Synchronous vs Asynchronous Communication
domain: Microservices
module: Fundamentals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - microservices
related:
  - "[[Service Communication]]"
  - "[[REST vs gRPC]]"
---

# Synchronous vs Asynchronous Communication

## Overview
**Synchronous**: the caller sends a request and blocks for the response (REST, gRPC). **Asynchronous**: the caller publishes a message/event and moves on; a broker delivers it later (Kafka, RabbitMQ).

## Why It Matters
This is the highest-leverage coupling decision. Sync chains create cascading failures and latency stacking; async decouples but forces you to handle eventual consistency and ordering.

## Comparison
| | Synchronous | Asynchronous |
|--|-------------|--------------|
| Timing | caller waits | fire-and-forget |
| Coupling | temporal (both up) | decoupled |
| Failure | propagates immediately | absorbed by broker/retry |
| Latency | adds up across hops | producer unaffected |
| Consistency | immediate | eventual |
| Complexity | simple to reason about | ordering, dedup, DLQ |

## Trade-offs In Practice
- **Sync** is fine for a quick read where the caller genuinely needs the answer now (e.g., validate before commit).
- **Async** shines for propagating state changes ("order placed") to many consumers without coupling them to the producer's availability.
- Long sync call chains multiply latency and failure probability — break them with events.

## Patterns
- **Request/response** (sync), **event notification** and **event-carried state transfer** (async).
- Combine: sync for the command, async events for downstream effects.

## Interview Questions
- **When async over sync?** For decoupling, resilience, and fan-out of state changes; when the caller doesn't need an immediate result.
- **Downside of long synchronous chains?** Latency stacks and one slow/failed service cascades — mitigate with timeouts and circuit breakers.
- **What consistency do you get with async?** Eventual — you must handle ordering, duplicates ([[Idempotency]]), and failures ([[Dead Letter Queue|DLQ]]).

## Related Topics
- [[REST vs gRPC]] · [[Event-Driven Architecture]] · [[Eventual Consistency]] · [[Circuit Breaker]]

## Quick Revision
- Sync = wait, coupled, immediate, latency stacks. Async = broker, decoupled, resilient, eventual. Use sync for needed-now reads; async for state propagation/fan-out.
