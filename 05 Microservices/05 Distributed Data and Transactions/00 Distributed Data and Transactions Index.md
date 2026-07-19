---
title: Distributed Data and Transactions Index
aliases:
  - Distributed Data and Transactions Index
domain: Microservices
module: Distributed Data and Transactions
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - microservices
  - index
related:
  - "[[Microservices Index|Microservices]]"
  - "[[Distributed Transactions]]"
  - "[[Saga Pattern]]"
  - "[[Outbox Pattern]]"
  - "[[Idempotency]]"
---

# Distributed Data and Transactions

> Module index - part of the [[Microservices Index|Microservices]] learning path.

## Overview
With a database per service, a single business operation spans multiple services and databases — you can't use one ACID transaction. This module covers how to keep data correct anyway: **sagas** for multi-step workflows, the **outbox** for reliable event publishing, **eventual consistency** as the model, and **idempotency** to survive retries/duplicates. This is the hardest microservices area and a heavy interview focus.

## Branches (expand each)
- **[[Distributed Transactions]]** — why 2PC is avoided.
  - [[Saga Pattern]] — local transactions + compensations.
    - [[Orchestration Saga]] — central coordinator.
    - [[Choreography Saga]] — event-driven, no coordinator.
- **[[Outbox Pattern]]** — atomically persist + publish events.
- **[[Eventual Consistency]]** — the consistency model you accept.
- **[[Idempotency]]** — safe reprocessing of duplicates.

## Learning Roadmap
1. [[Distributed Transactions]] -> [[Saga Pattern]] -> [[Orchestration Saga]] / [[Choreography Saga]]
2. [[Outbox Pattern]]
3. [[Eventual Consistency]] -> [[Idempotency]]

## Prerequisites
- [[Resilience Index|Resilience]]

## Related
- [[Microservices Index|Microservices]]
- Next: [[Event-Driven Index|Event-Driven]]

## Quick Revision
- No cross-service ACID -> sagas (local tx + compensation), outbox (reliable publish), eventual consistency, idempotency for duplicates. Avoid 2PC.
