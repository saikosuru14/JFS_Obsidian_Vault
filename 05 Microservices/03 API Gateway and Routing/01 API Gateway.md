---
title: API Gateway
aliases:
  - API Gateway
domain: Microservices
module: API Gateway and Routing
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - microservices
related:
  - "[[API Gateway and Routing Index|API Gateway and Routing]]"
  - "[[Spring Cloud Gateway]]"
---

# API Gateway

## Overview
An API gateway is the single entry point between external clients and internal services. It centralizes cross-cutting concerns — routing, authentication, rate limiting, request aggregation, TLS termination, logging — so individual services stay focused on business logic.

## Why It Matters
Without a gateway, every client must know service topology and every service re-implements auth/rate-limiting. The gateway decouples clients from internal structure and enforces policy in one place.

## Responsibilities
- **Routing** — map external paths to internal services.
- **Auth** — validate JWT/OAuth tokens at the edge; pass identity downstream.
- **Rate limiting / throttling** — protect backends from abuse ([[Rate Limiting]]).
- **Aggregation** — combine multiple service calls into one response (or use BFF).
- **Cross-cutting** — TLS termination, CORS, logging, tracing headers, response caching.

## Patterns & Cautions
- **BFF (Backend for Frontend)** — a gateway tailored per client type (web/mobile).
- **Don't put business logic in the gateway** — it becomes a bottleneck and a coupling point.
- It's a single point of failure — run it **highly available** behind an LB.

## Options
[[Spring Cloud Gateway]], Kong, NGINX, AWS API Gateway, Envoy.

## Interview Questions
- **What does an API gateway do?** Central edge for routing, auth, rate limiting, aggregation, and cross-cutting concerns.
- **Gateway vs load balancer?** A gateway is L7 with rich routing/policy/auth; an LB mainly distributes traffic.
- **Risk of a gateway?** Single point of failure and a place logic creeps into — keep it HA and thin.

## Related Topics
- [[Spring Cloud Gateway]] · [[Load Balancing]] · [[Rate Limiting]] · [[Circuit Breaker]]

## Quick Revision
- Single edge entry: routing, auth, rate limit, aggregation, TLS/logging. Keep it thin + HA. Not a place for business logic. BFF = per-client gateway.
