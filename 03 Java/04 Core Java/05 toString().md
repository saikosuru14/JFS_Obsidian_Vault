---
title: toString()
aliases:
  - toString()
domain: Java
module: Core Java
status: Not Started
difficulty: Easy
priority: Low
interview: 2
revision: Monthly
order: 5
tags:
  - java
  - core
related:
  - "[[Object Class]]"
---

# toString()

## Overview
Returns a human-readable representation of an object. Default is `ClassName@hexHash` — override it for meaningful logs and debugging.

## Why It Matters
Good `toString` output speeds up debugging and log analysis. It's the cheapest observability win in a codebase.

## Best Practices
- Include the fields that identify the object; keep it concise.
- Don't include secrets/PII (logs leak).
- `record` and Lombok `@ToString` generate it; IDEs can too.
- Avoid heavy computation or triggering lazy loads (JPA) inside `toString`.

## Common Mistakes
- Logging entities whose `toString` triggers lazy Hibernate collections → `LazyInitializationException` or N+1.
- Leaking passwords/tokens in `toString`.

## Interview Questions
- What does the default `toString` return?
- Risks of `toString` on JPA entities?

## Related Topics
- [[Object Class]]

## Quick Revision
- Override for readable logs; concise, no secrets, no lazy loads. Records/Lombok generate it.
