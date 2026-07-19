---
title: Object Lifecycle
aliases:
  - Object Lifecycle
domain: Java
module: Core Java
status: Not Started
difficulty: Easy
priority: Low
interview: 2
revision: Monthly
order: 2
tags:
  - java
  - core
related:
  - "[[Object Class]]"
  - "[[Garbage Collection Overview]]"
---

# Object Lifecycle

## Overview
An object's life from allocation to reclamation. Understanding it clarifies memory behavior and why `finalize` is unreliable.

## Phases
```
new → constructor runs → reachable (in use)
   → unreachable (no live references)
   → eligible for GC → collected (memory reclaimed)
```

## How It Works
- `new` allocates on the heap; fields default-initialized, then the constructor runs.
- An object is **reachable** while referenced from a GC root (stack, statics, etc.).
- When unreachable, it becomes eligible for GC; the collector reclaims it at an unspecified time.
- See [[Garbage Collection Overview]] for how reclamation happens.

## Best Practices
- Release references you no longer need (esp. in long-lived collections/caches) to avoid [[Memory Leaks in Java|leaks]].
- Use try-with-resources for external resources; don't rely on `finalize`/`Cleaner` for correctness.

## Interview Questions
- When does an object become eligible for GC?
- Why can't you predict when GC runs?
- Why is `finalize()` unreliable?

## Related Topics
- [[Object Class]] · [[Garbage Collection Overview]] · [[Memory Leaks in Java]]

## Quick Revision
- new → reachable → unreachable → eligible → collected. Drop references promptly; don't depend on finalize.
