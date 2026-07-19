---
title: Performance and Memory Best Practices
aliases:
  - Performance and Memory Best Practices
domain: Java
module: Best Practices
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - java
  - best-practices
  - performance
related:
  - "[[GC Tuning]]"
  - "[[Performance Profiling]]"
  - "[[Collections Framework]]"
---

# Performance and Memory Best Practices

## Overview
Practical rules to keep Java services fast and memory-efficient — without premature optimization.

## Rules
- **Measure first** — profile before changing anything ([[Performance Profiling]]).
- **Reduce allocation** — object churn drives GC. Reuse buffers, avoid needless autoboxing (`int` vs `Integer`).
- **Size collections** — pass initial capacity for large `HashMap`/`ArrayList` to avoid resizes ([[HashMap]], [[ArrayList]]).
- **Pick the right collection** — `ArrayList` vs `LinkedList`, `HashMap` vs `TreeMap`, `EnumMap` for enum keys.
- **Prefer primitives and streams-of-primitives** (`IntStream`) in hot paths.
- **Avoid `String` concatenation in loops** — use `StringBuilder` ([[StringBuilder]]).
- **Be careful with streams in hot loops** — clean, but a plain loop can be faster; measure.
- **Cache expensive results**, but bound the cache (avoid leaks — [[Memory Leaks in Java]]).
- **Minimize lock scope** — contention kills throughput ([[Synchronization]]).

## Common Mistakes
- Autoboxing in tight loops (`Long` keys, `Integer` sums).
- Unbounded caches / static collections leaking memory.
- Optimizing cold paths; ignoring the dominant cost.

## Interview Questions
- What drives GC pressure and how do you reduce it?
- `ArrayList` vs `LinkedList` in practice?
- Streams vs loops for performance?

## Related Topics
- [[GC Tuning]] · [[Performance Profiling]] · [[Collections Framework]]

## Quick Revision
- Measure → cut allocations → size collections → right data structure → StringBuilder → bounded caches → small lock scope.
