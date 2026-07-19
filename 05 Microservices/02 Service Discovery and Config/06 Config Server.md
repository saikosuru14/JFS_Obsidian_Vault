---
title: Config Server
aliases:
  - Config Server
domain: Microservices
module: Service Discovery and Config
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 6
tags:
  - microservices
related:
  - "[[Distributed Configuration]]"
  - "[[Config Client]]"
---

# Config Server

## Overview
Spring Cloud Config Server is a centralized configuration source, typically backed by a **Git** repository (also file system, Vault, JDBC). Clients fetch their config from it at startup, keyed by application name and profile.

## Why It Matters
It gives one auditable, versioned place for all service config, with per-environment profiles and runtime refresh — the Spring answer to distributed configuration.

## Setup
```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApp { }
```
```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/org/config-repo
```
Config files in the repo: `order-service.yml`, `order-service-prod.yml`, `application.yml` (shared).

## Key Features
- **Git-backed versioning** — history, branches per environment, rollback.
- **Profiles & labels** — resolve by `{app}-{profile}` and Git label/branch.
- **Encryption** — `{cipher}` values decrypted by the server (symmetric/asymmetric keys).
- **Refresh** — `/actuator/refresh` on clients, or broadcast via **Spring Cloud Bus**.

## Best Practices
- Secure the server (it holds sensitive config) and encrypt secrets or delegate to Vault.
- Make it highly available (multiple instances); clients cache last-known config.
- Keep a separate config repo with controlled access.

## Interview Questions
- **What backs a Config Server?** Usually Git (versioned), or Vault/JDBC/filesystem.
- **How are secrets protected?** `{cipher}` encrypted values or Vault integration; never plaintext.
- **How do clients pick their config?** By `spring.application.name` + active profile (+ Git label).

## Related Topics
- [[Config Client]] · [[Distributed Configuration]] · [[Spring Cloud]]

## Quick Revision
- Centralized, Git-backed config; `@EnableConfigServer`. Profiles/labels, encryption, refresh via actuator/Bus. Secure + HA; clients cache last-known.
