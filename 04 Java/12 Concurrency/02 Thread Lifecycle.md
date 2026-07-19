---
title: Thread Lifecycle
aliases:
  - Thread Lifecycle
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 2
tags:
  - java
related:
  - "[[Threads]]"
---

# Thread Lifecycle

## Overview
A Java thread moves through six states defined by `Thread.State`. Knowing them turns a confusing thread dump into an actionable diagnosis.

## States
| State | Meaning |
|-------|---------|
| NEW | Created, not yet `start()`ed |
| RUNNABLE | Eligible to run (running or waiting for CPU) |
| BLOCKED | Waiting to acquire a monitor lock (`synchronized`) |
| WAITING | Waiting indefinitely (`wait()`, `join()`, `park()`) |
| TIMED_WAITING | Waiting with timeout (`sleep`, `wait(ms)`, `join(ms)`) |
| TERMINATED | `run()` finished or threw |

## Transitions
```
NEW --start()--> RUNNABLE
RUNNABLE <--> BLOCKED        (lock contention)
RUNNABLE <--> WAITING        (wait/join/park + notify/unpark)
RUNNABLE <--> TIMED_WAITING  (sleep/timed wait)
RUNNABLE --> TERMINATED
```

## Why It Matters
In a thread dump: many threads `BLOCKED` on the same lock signals contention; many `WAITING` on a pool queue signals an undersized pool or a downstream stall; `TIMED_WAITING` in `sleep` often points to busy-wait anti-patterns.

## Best Practices
- Use `jstack` / thread dumps to read live states during incidents.
- `RUNNABLE` in the JVM can still be blocked on native I/O — don't assume it means CPU-bound.

## Interview Questions
- **BLOCKED vs WAITING?** BLOCKED waits for a monitor lock; WAITING waits for another thread to signal (`notify`/`unpark`).
- **Can a thread go from TERMINATED back to RUNNABLE?** No — a thread runs once; you cannot restart it.

## Related Topics
- [[Threads]] · [[Synchronization]] · [[Deadlocks in Java]]

## Quick Revision
- Six states. BLOCKED = lock; WAITING/TIMED_WAITING = signal/timeout. Threads never restart.
