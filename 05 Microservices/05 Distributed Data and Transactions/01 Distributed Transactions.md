---
title: Distributed Transactions
aliases:
  - Distributed Transactions
domain: Microservices
module: Distributed Data and Transactions
status: Learning
difficulty: Hard
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - microservices
related:
  - "[[Distributed Data and Transactions Index|Distributed Data and Transactions]]"
  - "[[Saga Pattern]]"
---

# Distributed Transactions

## Overview
A distributed transaction spans multiple services/databases. Classic ACID guarantees don't extend across network boundaries cheaply, so microservices avoid two-phase commit (2PC) and instead use patterns that accept eventual consistency.

## Why It Matters
"How do you keep data consistent across services?" is the defining microservices question. The expected answer is sagas + outbox + idempotency, and *why not 2PC*.

## Why Avoid 2PC / XA
- **Blocking + locks held across the network** — coordinator failure can leave resources locked.
- **Poor availability** — violates the AP preference of most microservices (CAP).
- **Tight coupling** — all participants must support XA and be up simultaneously.
- **Doesn't scale** — latency and contention grow with participants.

## The Alternatives
| Approach | Idea | Use |
|----------|------|-----|
| **[[Saga Pattern]]** | sequence of local transactions with compensations | multi-step business workflows |
| **[[Outbox Pattern]]** | atomic DB write + reliable event publish | avoid dual-write/lost events |
| **[[Eventual Consistency]]** | converge over time | accept temporary divergence for availability |

## Guiding Principle
Model the operation as local ACID transactions in each service, connected by events, and make each step **[[Idempotency|idempotent]]** and compensatable rather than one global transaction.

## Interview Questions
- **Why not use 2PC in microservices?** Blocking, holds locks across the network, hurts availability, couples services, and scales poorly.
- **How do you achieve consistency instead?** Sagas (local tx + compensation), the outbox for reliable publishing, idempotency, and eventual consistency.
- **What consistency do you end up with?** Eventual — brief windows of divergence in exchange for availability.

## Related Topics
- [[Saga Pattern]] · [[Outbox Pattern]] · [[Eventual Consistency]] · [[Idempotency]]

## Quick Revision
- No cheap cross-service ACID. Avoid 2PC (blocking, low availability, coupling). Use sagas + outbox + idempotency; accept eventual consistency.
