---
title: Distributed Configuration
aliases:
  - Distributed Configuration
domain: Microservices
module: Service Discovery and Config
status: Learning
difficulty: Medium
priority: High
interview: 3
revision: Weekly
order: 5
tags:
  - microservices
related:
  - "[[Service Discovery and Config Index|Service Discovery and Config]]"
  - "[[Config Server]]"
---

# Distributed Configuration

## Overview
Distributed configuration externalizes settings out of the code/artifact so they can vary per environment and change without redeploying. Config is versioned, centralized, and delivered to services at startup and (optionally) refreshed at runtime.

## Why It Matters
Hardcoded or baked-in config forces rebuilds for every change and leaks secrets into artifacts. Externalized config is a **12-Factor** requirement and enables safe promotion across environments.

## Principles
- **Externalize** everything environment-specific (URLs, credentials, feature flags).
- **Never commit secrets** in plaintext — use a secrets manager (Vault, AWS Secrets Manager) or encrypted values.
- **Environment profiles** — `application-{dev,stage,prod}.yml`; one artifact, many environments.
- **Version config** — store in Git so changes are auditable and revertible.
- **Refresh** — support runtime updates without full redeploy (`@RefreshScope`, Spring Cloud Bus).

## Delivery Options
- **[[Config Server|Spring Cloud Config Server]]** — Git-backed centralized config.
- **Kubernetes** ConfigMaps + Secrets.
- **HashiCorp Vault / AWS Parameter Store** — secrets and dynamic credentials.

## Interview Questions
- **Why externalize configuration?** Change behavior per environment without rebuilding; keep secrets out of artifacts (12-Factor).
- **How do you handle secrets?** A secrets manager or encryption — never plaintext in Git.
- **How do config changes take effect without restart?** `@RefreshScope` + a refresh trigger (actuator/`Spring Cloud Bus`).

## Related Topics
- [[Config Server]] · [[Config Client]] · [[Spring Cloud]]

## Quick Revision
- Externalize + version config; secrets in a manager, never plaintext. Profiles per environment; refresh at runtime via `@RefreshScope`/Bus. 12-Factor config.
