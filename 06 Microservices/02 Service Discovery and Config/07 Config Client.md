---
title: Config Client
aliases:
  - Config Client
domain: Microservices
module: Service Discovery and Config
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 7
tags:
  - microservices
related:
  - "[[Config Server]]"
---

# Config Client

## Overview
A config client is a service that pulls its configuration from the [[Config Server]] during bootstrap, before the rest of the application context starts. It resolves config by its application name and active profile.

## Why It Matters
It's the consumer side of centralized config, including the ability to **refresh** properties at runtime without restarting.

## Setup
```yaml
spring:
  application:
    name: order-service
  config:
    import: "optional:configserver:http://config-server:8888"
```

## Runtime Refresh
```java
@RefreshScope          // beans re-created on refresh, picking up new values
@Component
class RateConfig {
    @Value("${pricing.rate}") private BigDecimal rate;
}
```
- Trigger per instance: `POST /actuator/refresh`.
- Broadcast to all instances: **Spring Cloud Bus** (over Kafka/RabbitMQ) fires a `RefreshRemoteApplicationEvent`.

## Notes
- Without `@RefreshScope`, values are read once at startup and won't change.
- Clients should tolerate the Config Server being down (fail-fast vs `optional:` import; cache last-known config).

## Interview Questions
- **How do you change config without restarting?** Annotate beans with `@RefreshScope` and hit `/actuator/refresh` (or broadcast via Spring Cloud Bus).
- **When is config loaded?** During bootstrap, before the main context, keyed by name + profile.
- **What if the Config Server is unavailable at startup?** Use `optional:` import and/or cached config so the service can still start.

## Related Topics
- [[Config Server]] · [[Distributed Configuration]] · [[Spring Cloud]]

## Quick Revision
- Pulls config at bootstrap by name+profile. `@RefreshScope` + `/actuator/refresh` (or Cloud Bus) for runtime updates. Tolerate server downtime with cache/optional import.
