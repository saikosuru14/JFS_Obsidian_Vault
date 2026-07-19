---
title: Spring Cloud Gateway
aliases:
  - Spring Cloud Gateway
domain: Microservices
module: API Gateway and Routing
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 2
tags:
  - microservices
related:
  - "[[API Gateway]]"
---

# Spring Cloud Gateway

## Overview
Spring Cloud Gateway is the Spring implementation of an [[API Gateway]], built on the **reactive** stack (Spring WebFlux / Netty). Routes are defined by **predicates** (match conditions) and **filters** (transformations), and it's the modern replacement for Zuul 1.

## Why It Matters
It's non-blocking, so it scales well at the edge, and it integrates natively with discovery, [[Resilience4j]], and rate limiting.

## Route Model
```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: orders
          uri: lb://order-service          # lb:// = load-balanced via discovery
          predicates:
            - Path=/api/orders/**
          filters:
            - RewritePath=/api/orders/(?<seg>.*), /$\{seg}
            - AddRequestHeader=X-Source, gateway
            - name: CircuitBreaker
              args: { name: ordersCB, fallbackUri: forward:/fallback }
```

- **Predicates**: `Path`, `Method`, `Header`, `Query`, `After/Before` (time).
- **Filters**: `RewritePath`, `AddRequestHeader`, `CircuitBreaker`, `RequestRateLimiter`, `Retry`.
- **`lb://`** integrates with service discovery + client-side load balancing.

## Notes
- Reactive/non-blocking — don't call blocking code in custom filters.
- Global filters apply to all routes (auth, logging, tracing).
- Pairs with Redis for `RequestRateLimiter`.

## Interview Questions
- **Predicates vs filters?** Predicates decide if a route matches; filters modify the request/response or add behavior.
- **Why is it reactive?** Built on WebFlux/Netty for non-blocking, high-concurrency edge traffic.
- **What replaced Zuul?** Spring Cloud Gateway (Zuul 1 was blocking and is deprecated).

## Related Topics
- [[API Gateway]] · [[Circuit Breaker]] · [[Rate Limiting]] · [[Load Balancing]]

## Quick Revision
- Reactive (WebFlux/Netty) gateway. Routes = predicates (match) + filters (transform). `lb://` for discovery. Integrates Resilience4j + rate limiting. Replaces Zuul.
