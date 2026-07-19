---
title: Load Balancing
aliases:
  - Load Balancing
domain: Microservices
module: API Gateway and Routing
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 4
tags:
  - microservices
related:
  - "[[API Gateway and Routing Index|API Gateway and Routing]]"
---

# Load Balancing

## Overview
Load balancing distributes requests across multiple instances of a service to improve throughput, availability, and to avoid overloading any one instance. It can happen on the **client** side or the **server** side.

## Why It Matters
It's how horizontal scaling actually delivers capacity and resilience. The client-side vs server-side distinction (and where discovery fits) is a standard interview point.

## Client-side vs Server-side
| | Client-side | Server-side |
|--|-------------|-------------|
| Who decides | the caller (has instance list) | a dedicated LB/proxy |
| Example | Spring Cloud LoadBalancer | NGINX, AWS ELB, K8s Service |
| Needs discovery | yes (registry) | LB handles it |
| Extra hop | no | yes (through LB) |

## Algorithms
- **Round robin** — even rotation (default).
- **Least connections** — send to the least busy instance.
- **Weighted** — bias toward more capable instances.
- **Consistent hashing** — sticky routing by key (useful for caches/sessions).

## In Spring
Spring Cloud LoadBalancer (client-side) replaced Netflix Ribbon. `lb://service-name` in the gateway and `@FeignClient` names both go through it, using the discovery registry.

## Best Practices
- Combine with [[Health Checks]] so only healthy instances get traffic.
- On Kubernetes, the platform's Service/kube-proxy does server-side balancing.

## Interview Questions
- **Client-side vs server-side load balancing?** Caller picks the instance (needs discovery) vs a proxy/LB distributes (extra hop).
- **Common algorithms?** Round robin, least connections, weighted, consistent hashing.
- **What replaced Ribbon?** Spring Cloud LoadBalancer.

## Related Topics
- [[Service Discovery]] · [[Health Checks]] · [[API Gateway]] · [[OpenFeign]]

## Quick Revision
- Spread traffic across instances. Client-side (Spring Cloud LoadBalancer + discovery) vs server-side (NGINX/ELB/K8s). Algorithms: round robin, least-conn, weighted, consistent hash. Pair with health checks.
