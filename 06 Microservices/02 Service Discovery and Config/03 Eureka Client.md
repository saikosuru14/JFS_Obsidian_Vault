---
title: Eureka Client
aliases:
  - Eureka Client
domain: Microservices
module: Service Discovery and Config
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 3
tags:
  - microservices
related:
  - "[[Service Discovery]]"
  - "[[Eureka Server]]"
---

# Eureka Client

## Overview
A Eureka client is any service that **registers itself** with the registry on startup and **fetches** the registry to discover other services. Modern Spring Cloud auto-configures this when the discovery dependency is present.

## Why It Matters
It's the consumer side of discovery — how a service both advertises itself and resolves peers by logical name for load-balanced calls.

## Setup
```java
@SpringBootApplication          // @EnableDiscoveryClient is optional now (auto-configured)
public class OrderServiceApp { }
```
```yaml
spring:
  application:
    name: order-service         # the logical name others look up
eureka:
  client:
    service-url:
      defaultZone: http://eureka:8761/eureka/
```

## How It Works
- Registers `order-service` with host/port; renews its lease via heartbeats.
- Caches the registry locally and refreshes periodically (tolerates brief registry downtime).
- Calls peers by name (`http://inventory-service/...`) through a load balancer, not a fixed URL.

## With Load Balancing
Combine with **Spring Cloud LoadBalancer** (or [[OpenFeign]]) so `http://inventory-service` resolves to a healthy instance automatically. See [[Load Balancing]].

## Interview Questions
- **How does a client discover services?** It fetches the registry (cached locally) and resolves logical names to instances, then load-balances.
- **What happens if Eureka is briefly down?** Clients use their cached registry, so calls keep working for a while.
- **What names a service in the registry?** `spring.application.name`.

## Related Topics
- [[Eureka Server]] · [[Service Discovery]] · [[Load Balancing]] · [[OpenFeign]]

## Quick Revision
- Registers self + fetches registry; named by `spring.application.name`. Caches registry (survives brief Eureka outage). Resolves names via load balancer.
