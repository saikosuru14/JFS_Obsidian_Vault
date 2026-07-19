---
title: Orchestration Saga
aliases:
  - Orchestration Saga
domain: Microservices
module: Distributed Data and Transactions
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - microservices
related:
  - "[[Saga Pattern]]"
  - "[[Choreography Saga]]"
---

# Orchestration Saga

## Overview
In an orchestration saga, a central **orchestrator** (a dedicated service or state machine) explicitly drives each step: it sends a command, waits for the reply, then decides the next step or triggers compensation. It owns the workflow state.

## Why It Matters
It makes complex, multi-step workflows explicit and observable — you can see exactly where a saga is and why. Favored for anything with branching logic.

## How It Works
```
Orchestrator
  -> Payment.charge  -> ok
  -> Inventory.reserve -> FAIL
  -> Payment.refund (compensation)
  -> Order.cancel
```
The orchestrator persists saga state so it can resume after a crash. Tools: Camunda, Netflix Conductor, Temporal, or a hand-rolled state machine.

## Pros / Cons
| Pros | Cons |
|------|------|
| Centralized, explicit flow | Extra service to build/run |
| Easy to monitor & debug | Orchestrator can become a coupling hub |
| Clear compensation logic | Slight central dependency |

## When To Use
- Complex workflows with conditional branching, many steps, or strong monitoring needs.

## Interview Questions
- **What is an orchestration saga?** A central coordinator issues commands and manages the workflow + compensations.
- **Trade-off vs choreography?** Easier to monitor/change but adds a central service and potential coupling.
- **How does it survive crashes?** Persists saga state and resumes.

## Related Topics
- [[Choreography Saga]] · [[Saga Pattern]] · [[Distributed Transactions]]

## Quick Revision
- Central orchestrator drives steps + compensation, owns/persists state. Explicit, observable, good for complex flows; cost = extra service + central dependency.
