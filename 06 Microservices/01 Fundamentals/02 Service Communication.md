---
title: Service Communication
aliases:
  - Service Communication
domain: Microservices
module: Fundamentals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - microservices
related:
  - "[[Fundamentals Index|Fundamentals]]"
  - "[[Synchronous vs Asynchronous Communication]]"
---

# Service Communication

## Overview
Services communicate either **synchronously** (request/response over REST or gRPC) or **asynchronously** (messages/events over Kafka or RabbitMQ). This sub-hub frames the choice; the details are in the child notes.

## Why It Matters
Communication style determines coupling, latency, failure modes, and how you achieve consistency. Getting it wrong creates chatty, fragile systems (distributed monoliths).

## The Landscape
- **[[Synchronous vs Asynchronous Communication|Synchronous]]** — caller waits; temporal coupling; simple but propagates failures. Protocols compared in [[REST vs gRPC]].
- **[[Synchronous vs Asynchronous Communication|Asynchronous]]** — fire-and-forget via a broker; decoupled, resilient; needs eventual-consistency handling.

## Interaction Styles
| Style | Example | Coupling |
|-------|---------|----------|
| One-to-one, sync | REST call, gRPC | high (temporal) |
| One-to-one, async | command queue | medium |
| One-to-many, async | pub/sub events | low |

## Anti-Patterns
- **Distributed monolith** — services so chatty/synchronously-coupled that they must deploy together.
- **Chatty APIs** — many fine-grained calls per operation; batch or redesign boundaries.

## Best Practices
- Prefer async events for cross-service state propagation to reduce coupling.
- Use sync only when you truly need an immediate answer.
- Design for partial failure: timeouts, retries, circuit breakers ([[Resilience Index|Resilience]]).

## Interview Questions
- **How do microservices communicate?** Sync (REST/gRPC) for immediate responses, async (Kafka/RabbitMQ) for decoupled event flows.
- **What is a distributed monolith?** Services coupled so tightly (usually via sync calls) that independent deployment is lost — the worst of both worlds.
- **How do you choose the style?** By coupling, latency needs, and reliability — favor async for state propagation.

## Related Topics
- [[Synchronous vs Asynchronous Communication]] · [[REST vs gRPC]] · [[Event-Driven Architecture]]

## Quick Revision
- Sync (REST/gRPC) = immediate, coupled; async (broker) = decoupled, resilient. Avoid distributed monoliths and chatty APIs; design for partial failure.
