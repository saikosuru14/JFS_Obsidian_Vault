---
title: Saga Pattern
aliases:
  - Saga Pattern
domain: Microservices
module: Distributed Data and Transactions
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 2
tags:
  - microservices
related:
  - "[[Distributed Transactions]]"
  - "[[Orchestration Saga]]"
  - "[[Choreography Saga]]"
---

# Saga Pattern

## Overview
A saga models a business transaction as a **sequence of local transactions**, one per service. Each step publishes an event/command triggering the next. If a step fails, the saga runs **compensating transactions** to semantically undo the completed steps — there is no global rollback.

## Why It Matters
It's the primary way to maintain data integrity across services without 2PC, and the most-asked distributed-data interview topic.

## How It Works
```
Order -> Payment -> Inventory -> Shipping
  each = a local ACID transaction + an event

If Inventory fails:
  compensate Payment (refund), compensate Order (cancel)
```
- **Compensation** is semantic, not a rollback — e.g., "refund" undoes "charge," it doesn't erase history.
- Steps must be **[[Idempotency|idempotent]]** (events can be redelivered).

## Two Coordination Styles
- **[[Orchestration Saga]]** — a central orchestrator tells each service what to do and tracks state.
- **[[Choreography Saga]]** — services react to each other's events; no central coordinator.

## Design Notes
- Not isolated: intermediate states are visible (no ACID isolation) — design for it (e.g., "pending" states).
- Model compensations up front; some actions are hard to undo (send email) — use pending/confirm.

## Interview Questions
- **What is a saga?** A sequence of local transactions with compensating actions for failures, replacing distributed ACID.
- **Rollback vs compensation?** Rollback erases; compensation performs a semantic inverse (refund vs un-charge).
- **Orchestration vs choreography?** Central coordinator vs decentralized event reactions.
- **Key challenge?** No isolation — intermediate states are visible; steps must be idempotent.

## Related Topics
- [[Orchestration Saga]] · [[Choreography Saga]] · [[Outbox Pattern]] · [[Idempotency]]

## Quick Revision
- Chain of local transactions + compensations (semantic undo), no global rollback. Steps idempotent; no isolation. Coordinate via orchestration or choreography.
