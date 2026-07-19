---
title: Object Class
aliases:
  - Object Class
domain: Java
module: Core Java
status: Not Started
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
  - core
related:
  - "[[Java]]"
  - "[[equals() vs ==]]"
  - "[[hashCode()]]"
---

# Object Class

## Overview
`java.lang.Object` is the root of every class hierarchy. Its methods underpin collections, concurrency, and framework behavior.

## Key Methods
| Method | Purpose |
|--------|---------|
| `equals(Object)` | logical equality (override with `hashCode`) |
| `hashCode()` | bucket placement in hash collections |
| `toString()` | debug/log representation |
| `getClass()` | runtime type (used in reflection) |
| `clone()` | field copy (via `Cloneable`) |
| `wait/notify/notifyAll` | intrinsic-lock coordination |
| `finalize()` | deprecated — never rely on it |

## Why It Matters
`equals`/`hashCode` correctness drives [[HashMap]]/[[HashSet]], JPA/Hibernate identity, and deduplication. `wait/notify` are the low-level basis of monitors (see [[Synchronization]]).

## Best Practices
- Override `equals` and `hashCode` **together**; keep them consistent with each other.
- Provide a useful `toString` for domain objects.
- Prefer higher-level concurrency utilities over raw `wait/notify`.
- Never use `finalize()`; use try-with-resources / `Cleaner`.

## Interview Questions
- Which `Object` methods matter for collections and why?
- Why is `finalize()` discouraged?
- What do `wait`/`notify` require to be called safely? (holding the monitor)

## Related Topics
- [[equals() vs ==]] · [[hashCode()]] · [[toString()]] · [[clone()]]

## Quick Revision
- Root class; equals/hashCode/toString/getClass/clone/wait-notify. Override equals+hashCode together; avoid finalize.
