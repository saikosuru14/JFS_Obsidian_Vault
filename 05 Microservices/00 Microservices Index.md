---
title: Microservices Index
aliases:
  - Microservices
  - Microservices Index
domain: Microservices
module: Index
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - microservices
  - index
---

# Microservices

> Domain hub — designing, connecting, and hardening distributed services.

## Overview
Microservices decompose a system into small, independently deployable services that communicate over the network. This raises new concerns: discovery, configuration, gateways, resilience, distributed data, eventing, and observability.

## Learning Roadmap
1. [[Fundamentals Index|Fundamentals]] — monolith vs microservices, communication styles, REST vs gRPC.
2. [[Service Discovery and Config Index|Service Discovery & Config]] — Eureka, Spring Cloud, centralized config.
3. [[API Gateway and Routing Index|API Gateway & Routing]] — gateway, Feign, client-side load balancing.
4. [[Resilience Index|Resilience]] — circuit breaker, retry, bulkhead, rate limiting.
5. [[Distributed Data and Transactions Index|Distributed Data & Transactions]] — Saga, Outbox, eventual consistency.
6. [[Event-Driven Index|Event-Driven]] — event architecture, ordering, versioning, DLQ.
7. [[Observability Index|Observability]] — distributed tracing and centralized logging.

## Suggested Study Order
Understand the fundamentals and communication trade-offs first, then the platform concerns (discovery, config, gateway), then reliability (resilience), and finally the hardest topics: distributed data, eventing, and observability.

## Prerequisites
- [[Spring]] — especially [[Spring Boot Index|Spring Boot]].
- [[System Design]] fundamentals.

## Related Concepts
- [[Apache Kafka]] — the backbone for event-driven microservices.
- [[Docker]] and [[Kubernetes]] — how services are packaged and run.

## Interview Focus
- Monolith vs microservices trade-offs.
- Service discovery and centralized configuration.
- Resilience patterns (circuit breaker, retry, bulkhead).
- Saga vs 2PC; the Outbox pattern; idempotency.
- Distributed tracing across services.

## Topic Tracker

> Live, auto-updating table of every note in this domain, grouped by module.

![[Microservices.base]]
