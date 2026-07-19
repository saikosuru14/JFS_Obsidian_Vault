---
title: Eventual Consistency
aliases:
  - Eventual Consistency
domain: Microservices
module: Distributed Data and Transactions
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 6
tags:
  - microservices
related:
  - "[[Distributed Data and Transactions Index|Distributed Data and Transactions]]"
  - "[[Saga Pattern]]"
---

# Eventual Consistency

## Overview
Eventual consistency means that, given no new updates, all replicas/services will **converge** to the same state over time — but there's a window where they diverge. It's the consistency model you accept in exchange for availability and partition tolerance (CAP: AP).

## Why It Matters
Every event-driven, saga-based microservice system is eventually consistent. Designing UX and logic around brief staleness — instead of pretending it's immediate — is the mark of experience.

## Why You Accept It
- **CAP** — under a network partition you choose availability (AP) over strict consistency (CP).
- Cross-service ACID is impractical (no cheap 2PC), so state propagates via events.

## Designing For It
- **Model intermediate states** explicitly ("pending", "processing").
- **Idempotent** consumers ([[Idempotency]]) to handle redelivery.
- **Read-your-writes** where needed via session stickiness or reading the source of truth.
- Communicate staleness in UX ("your order is being processed").
- Reconcile with periodic jobs for drift.

## Consistency Spectrum
Strong (single DB) -> Read-your-writes / monotonic reads -> Eventual. Choose the weakest model that satisfies the business requirement.

## Interview Questions
- **What is eventual consistency?** Replicas/services converge over time; temporary divergence is allowed.
- **Why accept it?** CAP — availability under partitions; cross-service ACID is impractical.
- **How do you handle it in UX/logic?** Pending states, idempotency, reconciliation, and communicating status.

## Related Topics
- [[Saga Pattern]] · [[Outbox Pattern]] · [[Idempotency]] · [[Event-Driven Architecture]]

## Quick Revision
- Converge over time, temporary divergence (CAP: AP). Design with pending states, idempotency, reconciliation. Pick the weakest sufficient consistency model.
