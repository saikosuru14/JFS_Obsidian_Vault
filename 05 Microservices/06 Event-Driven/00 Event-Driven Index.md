---
title: Event-Driven Index
aliases:
  - Event-Driven Index
domain: Microservices
module: Event-Driven
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 0
tags:
  - microservices
  - index
related:
  - "[[Microservices Index|Microservices]]"
  - "[[Event-Driven Architecture]]"
---

# Event-Driven

> Module index - part of the [[Microservices Index|Microservices]] learning path.

## Overview
Event-driven architecture decouples services by having them communicate through **events** on a broker (usually [[Apache Kafka|Kafka]]) rather than direct calls. That decoupling brings its own concerns: preserving **ordering**, evolving **event schemas** safely, and handling messages that can't be processed (**DLQ**).

## Branch (expand)
- **[[Event-Driven Architecture]]** — the model, benefits, event types.
  - [[Event Ordering]] — guarantees and partition keys.
  - [[Event Versioning]] — schema evolution + registry.
  - [[Dead Letter Queue]] — handling poison messages.

## Learning Roadmap
1. [[Event-Driven Architecture]]
2. [[Event Ordering]]
3. [[Event Versioning]]
4. [[Dead Letter Queue]]

## Prerequisites
- [[Distributed Data and Transactions Index|Distributed Data and Transactions]]

## Related
- [[Microservices Index|Microservices]] · [[Apache Kafka]]
- Next: [[Observability Index|Observability]]

## Quick Revision
- Communicate via events on a broker (decoupled, scalable). Manage ordering (partition key), schema evolution (registry, backward-compatible), and failures (DLQ).
