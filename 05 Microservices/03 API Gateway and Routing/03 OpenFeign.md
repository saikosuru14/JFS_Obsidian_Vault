---
title: OpenFeign
aliases:
  - OpenFeign
domain: Microservices
module: API Gateway and Routing
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 3
tags:
  - microservices
related:
  - "[[API Gateway and Routing Index|API Gateway and Routing]]"
  - "[[Load Balancing]]"
---

# OpenFeign

## Overview
OpenFeign is a **declarative** HTTP client: you define an interface annotated with the request mapping, and Spring generates the implementation. It integrates with service discovery, client-side load balancing, and Resilience4j.

## Why It Matters
It removes boilerplate `RestTemplate`/`WebClient` wiring for service-to-service calls and reads like a local method call while resolving targets by service name.

## Usage
```java
@FeignClient(name = "inventory-service")     // resolved via discovery + load balancer
public interface InventoryClient {
    @GetMapping("/api/stock/{sku}")
    StockDto getStock(@PathVariable String sku);
}
```
```java
@EnableFeignClients      // on a @Configuration/@SpringBootApplication
```

## Features
- **Discovery + LB** — `name` resolves through Eureka/K8s and [[Load Balancing|Spring Cloud LoadBalancer]].
- **Resilience** — wrap with Resilience4j (`fallback`) for circuit breaking/retry.
- **Custom config** — encoders/decoders, interceptors (propagate auth/trace headers), error decoders, timeouts.

## Cautions
- It's a **synchronous, blocking** client — beware call chains and set timeouts.
- Propagate correlation/trace headers via a `RequestInterceptor` for [[Distributed Tracing]].

## Interview Questions
- **What is OpenFeign?** A declarative REST client generated from an annotated interface.
- **How does it find the target service?** By `name` via discovery + client-side load balancing.
- **How do you add resilience?** Combine with Resilience4j (fallbacks, circuit breaker) and set timeouts.

## Related Topics
- [[Load Balancing]] · [[REST vs gRPC]] · [[Resilience4j]] · [[Distributed Tracing]]

## Quick Revision
- Declarative REST client from an interface (`@FeignClient`). Resolves by service name + load balancing; add Resilience4j + timeouts. Blocking — mind call chains.
