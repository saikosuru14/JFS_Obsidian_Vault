---
title: Event-Driven Architecture
aliases:
  - Event-Driven Architecture
domain: Microservices
module: Event-Driven
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - microservices
related:
  - "[[Event-Driven Index|Event-Driven]]"
  - "[[Event Ordering]]"
  - "[[Event Versioning]]"
  - "[[Dead Letter Queue]]"
---

# Event-Driven Architecture

## Overview
In event-driven architecture (EDA), services publish **events** ("something happened") to a broker; interested services subscribe and react. Producers don't know or wait for consumers, giving strong temporal decoupling. This is the sub-hub for eventing concerns.

## Why It Matters
EDA is how large microservice systems stay loosely coupled and scalable. It underpins sagas, CQRS, and real-time pipelines — and it's the async half of [[Service Communication]].

## Event Styles
- **Event notification** — thin "OrderPlaced(id)"; consumer calls back for details.
- **Event-carried state transfer** — event carries the data consumers need (no callback), reducing coupling.
- **Event sourcing** — persist state as an append-only log of events (advanced).

## Benefits & Costs
| Benefits | Costs |
|----------|-------|
| Loose coupling | Eventual consistency |
| Independent scaling | Harder to trace/debug |
| Resilience (broker buffers) | Ordering + duplicate handling |
| Easy fan-out | Schema evolution management |

## Backbone
Usually [[Apache Kafka|Kafka]] (durable log, replay, partitions) or RabbitMQ (routing, queues). Kafka's log enables replay and multiple independent consumers.

## Key Concerns (children)
- [[Event Ordering]] — guaranteed only within a partition.
- [[Event Versioning]] — evolve schemas without breaking consumers.
- [[Dead Letter Queue]] — isolate un-processable messages.

## Interview Questions
- **Benefits of EDA?** Loose coupling, scalability, resilience, fan-out — at the cost of eventual consistency and harder tracing.
- **Notification vs state-transfer events?** Thin pointer requiring a callback vs self-contained event carrying the data.
- **Why Kafka for EDA?** Durable, replayable log with partitions and independent consumer groups.

## Related Topics
- [[Event Ordering]] · [[Event Versioning]] · [[Dead Letter Queue]] · [[Apache Kafka]] · [[Choreography Saga]]

## Quick Revision
- Publish/subscribe events via a broker (Kafka), decoupled + scalable. Styles: notification, state-transfer, event sourcing. Manage ordering, versioning, DLQ; accept eventual consistency.
