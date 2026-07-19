---
title: Resilience Index
aliases:
  - Resilience Index
domain: Microservices
module: Resilience
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
  - "[[Resilience4j]]"
  - "[[Circuit Breaker]]"
  - "[[Health Checks]]"
---

# Resilience

> Module index - part of the [[Microservices Index|Microservices]] learning path.

## Overview
In a distributed system, dependencies **will** fail and slow down. Resilience patterns keep one failing service from cascading into a full outage: fail fast ([[Circuit Breaker]]), retry transient errors, isolate resources ([[Bulkhead]]), cap load ([[Rate Limiting]]), and report status ([[Health Checks]]). **Resilience4j** implements most of these in Spring.

## Branches (expand each)
- **[[Resilience4j]]** — the library providing the patterns.
  - [[Circuit Breaker]] — stop calling a failing dependency.
  - [[Retry]] — re-attempt transient failures.
  - [[Bulkhead]] — isolate resource pools.
  - [[Rate Limiting]] — cap request rate.
- **[[Health Checks]]** — liveness/readiness for orchestrators.

## Learning Roadmap
1. [[Circuit Breaker]] -> [[Resilience4j]]
2. [[Retry]] -> [[Bulkhead]] -> [[Rate Limiting]]
3. [[Health Checks]]

## Prerequisites
- [[API Gateway and Routing Index|API Gateway and Routing]]

## Related
- [[Microservices Index|Microservices]]
- Next: [[Distributed Data and Transactions Index|Distributed Data and Transactions]]

## Quick Revision
- Assume dependencies fail: circuit breaker (fail fast), retry (transient, idempotent only), bulkhead (isolate), rate limit (cap), health checks (orchestrator signals). Resilience4j implements them.
