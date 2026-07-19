---
title: Service Discovery
aliases:
  - Service Discovery
domain: Microservices
module: Service Discovery and Config
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - microservices
related:
  - "[[Service Discovery and Config Index|Service Discovery and Config]]"
  - "[[Eureka Server]]"
  - "[[Eureka Client]]"
---

# Service Discovery

## Overview
Service discovery lets services locate each other without hardcoded hosts/ports. Instances register in a **service registry** on startup and are looked up by logical name at call time — essential when instances scale up/down and get dynamic addresses (containers, cloud).

## Why It Matters
Hardcoded endpoints break the moment you autoscale or redeploy. Discovery + client-side load balancing is the standard fix, and interviewers ask about the two discovery patterns.

## Patterns
| Pattern | Who resolves | Example |
|---------|--------------|---------|
| **Client-side** | client queries registry, picks an instance, load-balances | Eureka + Spring Cloud LoadBalancer |
| **Server-side** | client hits a router/LB that resolves | Kubernetes Service, AWS ALB |

## How It Works
1. Instance starts and **registers** (name, host, port, health) with the registry.
2. Registry tracks liveness via **heartbeats**; dead instances are evicted.
3. A caller **looks up** the name and receives current instances to call.

## Registry Options
- **[[Eureka Server|Eureka]]** (Spring Cloud Netflix), **Consul**, **etcd**, **Kubernetes** built-in DNS/Services.

## Best Practices
- Combine with health checks so only healthy instances receive traffic.
- On Kubernetes, prefer the platform's native discovery over Eureka.
- Cache registry data client-side and tolerate brief staleness.

## Interview Questions
- **Client-side vs server-side discovery?** Client queries the registry and load-balances itself vs a router/LB resolves on the client's behalf.
- **How are dead instances removed?** Heartbeats/leases expire and the registry evicts them.
- **Do you still need Eureka on Kubernetes?** Usually not — K8s Services provide discovery natively.

## Related Topics
- [[Eureka Server]] · [[Eureka Client]] · [[Load Balancing]] · [[Health Checks]]

## Quick Revision
- Find services by name via a registry. Client-side (Eureka) vs server-side (K8s/ALB). Register -> heartbeat -> lookup. On K8s, use native discovery.
