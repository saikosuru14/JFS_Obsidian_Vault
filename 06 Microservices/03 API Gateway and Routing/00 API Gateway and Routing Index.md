---
title: API Gateway and Routing Index
aliases:
  - API Gateway and Routing Index
domain: Microservices
module: API Gateway and Routing
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
  - "[[API Gateway]]"
  - "[[OpenFeign]]"
  - "[[Load Balancing]]"
---

# API Gateway and Routing

> Module index - part of the [[Microservices Index|Microservices]] learning path.

## Overview
A gateway is the single entry point for clients, handling cross-cutting concerns (routing, auth, rate limiting, aggregation) so services don't repeat them. Internally, services still call each other — declaratively via **OpenFeign** and spread across instances via **load balancing**.

## Branches (expand each)
- **[[API Gateway]]** — the edge entry point and its responsibilities.
  - [[Spring Cloud Gateway]] — the reactive Spring implementation.
- **[[OpenFeign]]** — declarative service-to-service REST client.
- **[[Load Balancing]]** — spreading calls across instances.

## Learning Roadmap
1. [[API Gateway]] -> [[Spring Cloud Gateway]]
2. [[OpenFeign]]
3. [[Load Balancing]]

## Prerequisites
- [[Service Discovery and Config Index|Service Discovery and Config]]

## Related
- [[Microservices Index|Microservices]]
- Next: [[Resilience Index|Resilience]]

## Quick Revision
- Gateway = one edge for routing/auth/rate-limit/aggregation. Feign = declarative internal REST client. Load balancing (client vs server side) spreads calls across instances.
