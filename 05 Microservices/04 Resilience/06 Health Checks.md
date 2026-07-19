---
title: Health Checks
aliases:
  - Health Checks
domain: Microservices
module: Resilience
status: Learning
difficulty: Easy
priority: Medium
interview: 3
revision: Weekly
order: 6
tags:
  - microservices
related:
  - "[[Resilience Index|Resilience]]"
---

# Health Checks

## Overview
Health checks expose a service's status via HTTP endpoints so orchestrators and load balancers can decide whether to route traffic, restart, or wait. Spring Boot Actuator provides them out of the box.

## Why It Matters
Kubernetes and load balancers rely on health signals to keep traffic away from broken/warming instances. Confusing liveness with readiness is a common, damaging mistake.

## Liveness vs Readiness
| Probe | Question | Failure action |
|-------|----------|----------------|
| **Liveness** | is the app alive? | restart the pod |
| **Readiness** | can it serve traffic now? | remove from LB (no restart) |
| **Startup** | has it finished booting? | delay other probes |

Getting these wrong is dangerous: a failing **readiness** check should stop traffic, but if you wire that logic into **liveness**, Kubernetes will restart-loop a healthy-but-busy pod.

## Spring Boot Actuator
```
/actuator/health              # overall
/actuator/health/liveness     # K8s liveness group
/actuator/health/readiness    # K8s readiness group
```
Health indicators aggregate checks (DB, disk, broker, custom `HealthIndicator`).

## Best Practices
- Keep liveness cheap and dependency-free (don't fail liveness because a downstream is down — that causes restart loops).
- Put dependency checks in **readiness**, so a struggling instance is removed from rotation but not killed.

## Interview Questions
- **Liveness vs readiness?** Alive (restart on fail) vs ready to serve (remove from LB on fail).
- **Why not check dependencies in liveness?** A downstream outage would restart-loop all your healthy pods.
- **How does Spring expose these?** Actuator `/actuator/health` with liveness/readiness groups for Kubernetes.

## Related Topics
- [[Load Balancing]] · [[Service Discovery]] · [[Distributed Tracing]]

## Quick Revision
- Endpoints for orchestrators. Liveness (restart) vs readiness (remove from LB) vs startup. Keep liveness cheap; dependency checks in readiness. Spring Actuator `/actuator/health`.
