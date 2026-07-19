---
title: Eureka Server
aliases:
  - Eureka Server
domain: Microservices
module: Service Discovery and Config
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 2
tags:
  - microservices
related:
  - "[[Service Discovery]]"
  - "[[Eureka Client]]"
---

# Eureka Server

## Overview
Eureka Server (Spring Cloud Netflix) is a **service registry**: clients register here and query it to discover peers. It's AP in CAP terms — it favors availability over strict consistency.

## Why It Matters
It's the canonical Spring implementation of client-side discovery, and its self-preservation behavior is a common gotcha in interviews and incidents.

## Setup
```java
@SpringBootApplication
@EnableEurekaServer
public class RegistryApp { }
```
```yaml
# registry does not register with itself
eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
```

## Key Behaviors
- **Heartbeats/leases** — clients renew every 30s (default); missed renewals -> eviction.
- **Self-preservation** — if too many heartbeats are lost at once (suspecting a network partition, not real deaths), Eureka stops evicting to avoid wiping a healthy registry. Good for partitions, but can serve stale instances.
- **Peer replication** — run multiple Eureka nodes that replicate to each other for HA.

## Best Practices
- Run 2+ replicated Eureka nodes in production.
- Understand self-preservation before disabling it; tune only with care.
- Pair with client-side load balancing.

## Interview Questions
- **What is Eureka's self-preservation mode?** When mass heartbeat loss suggests a network issue, Eureka stops evicting instances to avoid deregistering healthy ones during a partition.
- **Is Eureka CP or AP?** AP — it prioritizes availability and may serve slightly stale data.
- **How do you make Eureka highly available?** Deploy multiple peer-replicated instances.

## Related Topics
- [[Eureka Client]] · [[Service Discovery]] · [[Spring Cloud]]

## Quick Revision
- Spring Cloud registry; `@EnableEurekaServer`. AP, heartbeat leases, self-preservation guards against partitions (can serve stale). Run peer-replicated for HA.
