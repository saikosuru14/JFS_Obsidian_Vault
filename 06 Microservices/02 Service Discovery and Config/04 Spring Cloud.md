---
title: Spring Cloud
aliases:
  - Spring Cloud
domain: Microservices
module: Service Discovery and Config
status: Learning
difficulty: Medium
priority: High
interview: 3
revision: Weekly
order: 4
tags:
  - microservices
related:
  - "[[Service Discovery and Config Index|Service Discovery and Config]]"
---

# Spring Cloud

## Overview
Spring Cloud is a set of libraries that add the distributed-systems building blocks on top of Spring Boot: service discovery, centralized config, gateway, client-side load balancing, resilience, and distributed tracing.

## Why It Matters
It's the de-facto toolkit for building microservices in the Spring ecosystem, wiring the patterns in this domain together with minimal boilerplate.

## Core Components
| Component | Role | Note |
|-----------|------|------|
| Netflix Eureka | service registry | [[Eureka Server]] / [[Eureka Client]] |
| Config Server | centralized config | [[Config Server]] |
| Spring Cloud Gateway | API gateway/routing | [[Spring Cloud Gateway]] |
| OpenFeign | declarative REST client | [[OpenFeign]] |
| LoadBalancer | client-side LB | [[Load Balancing]] |
| Resilience4j | circuit breaker/retry | [[Resilience4j]] |
| Sleuth / Micrometer Tracing | distributed tracing | [[Distributed Tracing]] |

## Notes
- Spring Cloud Netflix components (Ribbon, Hystrix, Zuul) are largely **deprecated**; the modern stack is **Spring Cloud LoadBalancer**, **Resilience4j**, and **Spring Cloud Gateway**.
- Versions align to Boot via the Spring Cloud release train (BOM).

## Interview Questions
- **What does Spring Cloud provide?** Discovery, config, gateway, load balancing, resilience, and tracing on top of Boot.
- **What replaced Hystrix/Ribbon/Zuul?** Resilience4j, Spring Cloud LoadBalancer, and Spring Cloud Gateway.
- **How are versions managed?** Via the Spring Cloud release-train BOM aligned to a Boot version.

## Related Topics
- [[Eureka Server]] · [[Config Server]] · [[Spring Cloud Gateway]] · [[Resilience4j]]

## Quick Revision
- Boot-based toolkit: Eureka, Config Server, Gateway, LoadBalancer, Resilience4j, tracing. Modern stack replaces deprecated Netflix Ribbon/Hystrix/Zuul. Versioned by release-train BOM.
