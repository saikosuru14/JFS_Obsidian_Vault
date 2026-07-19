---
title: Race Conditions
aliases:
  - Race Conditions
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 10
tags:
  - java
related:
  - "[[Threads]]"
  - "[[Synchronization]]"
---

# Race Conditions

## Overview
A race condition occurs when the correctness of a result depends on the relative timing of threads accessing shared mutable state without proper coordination. The bug is intermittent and often invisible under light load.

## Why It Matters
Race conditions cause the hardest production bugs: they pass tests, survive code review, and only surface under concurrency. Recognizing the shape ("read-modify-write on shared state") is the skill.

## Classic Example
```java
class Counter {
    private int count = 0;
    void inc() { count++; }   // read, +1, write - NOT atomic
}
```
Two threads calling `inc()` can both read the same value and write it back, losing an update. This is a **check-then-act / read-modify-write** race.

## Types
- **Read-modify-write** — `count++`, lazy init.
- **Check-then-act** — `if (map.get(k) == null) map.put(k, v);` (use `computeIfAbsent`).
- **Visibility** — one thread never sees another's write (fix with `volatile` / synchronization).

## Fixes (cheapest first)
- Don't share: confine state to one thread or use immutability.
- [[Atomic Classes]] for single-variable counters (`AtomicInteger`).
- [[Synchronization]] / [[Locks]] for compound actions.
- Concurrent collections (`ConcurrentHashMap.computeIfAbsent`) for map races.

## Common Mistakes
- Assuming `volatile` fixes a `count++` (it fixes visibility, not atomicity).
- Guarding reads but not writes (or using different locks).

## Interview Questions
- **Why isn't `count++` thread-safe?** It is three operations (read, increment, write); another thread can interleave between them.
- **Race condition vs data race?** A data race is unsynchronized access to a shared variable; a race condition is timing-dependent incorrectness — related but not identical.

## Related Topics
- [[Synchronization]] · [[Atomic Classes]] · [[volatile]] · [[Deadlocks in Java]]

## Quick Revision
- Timing-dependent bug on shared mutable state. Fix by not sharing, atomics, or locking the whole compound action.
