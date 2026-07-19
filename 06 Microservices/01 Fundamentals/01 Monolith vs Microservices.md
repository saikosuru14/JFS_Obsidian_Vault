---
title: Monolith vs Microservices
aliases:
  - Monolith vs Microservices
domain: Microservices
module: Fundamentals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - microservices
related:
  - "[[Fundamentals Index|Fundamentals]]"
  - "[[Service Communication]]"
---

# Monolith vs Microservices

## Overview
A monolith is one deployable unit sharing a codebase and database. Microservices split the system into small, independently deployable services, each owning its data. The choice is an organizational and operational trade-off, not just a technical one.

## Why It Matters
Choosing microservices prematurely is a classic, expensive mistake — you pay distributed-systems tax (network failures, eventual consistency, ops overhead) before you have the scale or team size to benefit. Interviewers probe whether you know *when not to*.

## Comparison
| Aspect | Monolith | Microservices |
|--------|----------|---------------|
| Deployment | one unit | independent per service |
| Scaling | whole app | per service |
| Data | shared DB | database-per-service |
| Fault isolation | weak (one crash = all) | strong (blast radius contained) |
| Consistency | ACID transactions | eventual, [[Saga Pattern|sagas]] |
| Ops complexity | low | high (discovery, tracing, CI/CD) |
| Team fit | small, single team | many autonomous teams |

## When to Use Microservices
- Multiple teams needing to deploy independently.
- Parts of the system have very different scaling or availability needs.
- The domain has clear bounded contexts (DDD).

## When NOT To (start monolith-first)
- Early-stage product / unclear domain boundaries.
- Small team — you'll drown in ops.
- A well-modularized ("modular monolith") solves it more cheaply.
Migrate later using the **Strangler Fig** pattern: peel off services incrementally.

## Interview Questions
- **When should you NOT choose microservices?** Small teams, early-stage/unclear domains, or when a modular monolith suffices — the distributed tax outweighs the benefits.
- **Biggest challenge microservices introduce?** Distributed data consistency and operational complexity (network, discovery, tracing).
- **How do you migrate a monolith?** Strangler Fig — incrementally extract bounded contexts behind a facade/gateway.

## Related Topics
- [[Service Communication]] · [[Distributed Transactions]] · [[Saga Pattern]]

## Quick Revision
- Monolith: one unit, shared DB, simple ops, ACID. Microservices: independent deploy/scale, DB-per-service, eventual consistency, heavy ops. Start monolith-first; split by bounded context when teams/scale demand it.
