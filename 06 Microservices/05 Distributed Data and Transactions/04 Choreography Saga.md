---
title: Choreography Saga
aliases:
  - Choreography Saga
domain: Microservices
module: Distributed Data and Transactions
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 4
tags:
  - microservices
related:
  - "[[Saga Pattern]]"
  - "[[Orchestration Saga]]"
---

# Choreography Saga

## Overview
In a choreography saga there is **no central coordinator**. Each service listens for events, does its local transaction, and emits its own event that the next service reacts to. The workflow emerges from the chain of events.

## Why It Matters
It's the most decoupled saga style and fits event-driven systems naturally — but the lack of a central view makes complex flows hard to follow.

## How It Works
```
Order  --OrderCreated-->  Payment  --PaymentDone-->  Inventory  --Reserved-->  Shipping
On failure: emit a failure event; upstream services react with compensations.
```
Each service subscribes to relevant events (via [[Event-Driven Architecture|Kafka/broker]]) and owns its piece of the flow.

## Pros / Cons
| Pros | Cons |
|------|------|
| Fully decentralized, loosely coupled | Hard to trace end-to-end flow |
| No single point of coordination | Implicit workflow spread across services |
| Simple for short flows | Risk of cyclic event dependencies |

## When To Use
- Short, simple flows (2–4 steps) where decoupling matters more than central visibility.

## Making It Debuggable
- Use a correlation/saga id on every event and rely on [[Distributed Tracing]] to reconstruct flows.

## Interview Questions
- **What is a choreography saga?** Services react to each other's events without a coordinator; the flow is emergent.
- **Orchestration vs choreography — when each?** Choreography for simple, decoupled flows; orchestration for complex, monitored ones.
- **Main downside?** Hard to trace/reason about the overall flow; risk of event cycles.

## Related Topics
- [[Orchestration Saga]] · [[Saga Pattern]] · [[Event-Driven Architecture]] · [[Distributed Tracing]]

## Quick Revision
- No coordinator; services react to events and emit the next. Decoupled, great for short flows; hard to trace complex ones. Use correlation ids + tracing.
