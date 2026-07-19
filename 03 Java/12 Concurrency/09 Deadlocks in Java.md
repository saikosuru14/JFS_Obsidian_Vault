---
title: Deadlocks in Java
aliases:
  - Deadlocks in Java
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 9
tags:
  - java
related:
  - "[[Synchronization]]"
  - "[[Locks]]"
---

# Deadlocks in Java

## Overview
A deadlock is a cycle of threads each holding a lock the next one needs, so none can proceed. Related pathologies: **livelock** (threads keep reacting but make no progress) and **starvation** (a thread never gets scheduled/lock).

## Coffman Conditions
All four must hold; break any one to prevent deadlock:
1. **Mutual exclusion** — a resource is held exclusively.
2. **Hold and wait** — hold one lock while waiting for another.
3. **No preemption** — locks can't be forcibly taken.
4. **Circular wait** — a cycle in the wait-for graph.

## Classic Example
```java
// Thread 1: lock(A) then lock(B)
// Thread 2: lock(B) then lock(A)   <-- reverse order => deadlock
```

## Prevention (most practical first)
- **Global lock ordering** — always acquire locks in the same order (e.g., by object hash/id). Breaks circular wait.
- **`tryLock(timeout)`** — back off and retry instead of blocking forever. Breaks hold-and-wait.
- **Reduce lock scope** — hold fewer locks, for less time; avoid nested locks.
- **Use higher-level tools** — concurrent collections / atomics that lock internally.

## Detection
- Thread dump (`jstack`) — the JVM prints "Found one Java-level deadlock" with the cycle.
- `ThreadMXBean.findDeadlockedThreads()` at runtime.

## Interview Questions
- **Four conditions for deadlock?** Mutual exclusion, hold-and-wait, no preemption, circular wait.
- **Simplest way to prevent it?** Impose a global lock-acquisition order.
- **Deadlock vs livelock?** Deadlock: threads blocked forever. Livelock: threads active but repeatedly undoing each other's progress.

## Related Topics
- [[Locks]] · [[Synchronization]] · [[Thread Lifecycle]]

## Quick Revision
- Four Coffman conditions; break any one. Fix in practice with consistent lock ordering or tryLock timeouts. Diagnose via jstack.
