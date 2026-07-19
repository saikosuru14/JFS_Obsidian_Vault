---
title: Service Discovery and Config Index
aliases:
  - Service Discovery and Config Index
domain: Microservices
module: Service Discovery and Config
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
  - "[[Service Discovery]]"
  - "[[Spring Cloud]]"
  - "[[Distributed Configuration]]"
---

# Service Discovery and Config

> Module index - part of the [[Microservices Index|Microservices]] learning path.

## Overview
In a dynamic environment, service instances come and go with changing addresses. **Service discovery** lets services find each other by name; **distributed configuration** externalizes settings so you can change them without redeploying. Spring Cloud provides both (Eureka + Config Server).

## Branches (expand each)
- **[[Service Discovery]]** — dynamic instance lookup.
  - [[Eureka Server]] — the registry.
  - [[Eureka Client]] — register + discover.
- **[[Spring Cloud]]** — the umbrella toolkit tying these together.
- **[[Distributed Configuration]]** — externalized, versioned config.
  - [[Config Server]] — centralized config source.
    - [[Config Client]] — consumes config, refreshes at runtime.

## Learning Roadmap
1. [[Service Discovery]] -> [[Eureka Server]] -> [[Eureka Client]]
2. [[Spring Cloud]]
3. [[Distributed Configuration]] -> [[Config Server]] -> [[Config Client]]

## Prerequisites
- [[Fundamentals Index|Fundamentals]]

## Related
- [[Microservices Index|Microservices]]
- Next: [[API Gateway and Routing Index|API Gateway and Routing]]

## Quick Revision
- Discovery = find instances by name (Eureka registry + clients). Config = externalized, versioned settings (Config Server + `@RefreshScope` clients). Spring Cloud ties it together.
