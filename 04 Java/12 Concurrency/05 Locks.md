---
title: Locks
aliases:
  - Locks
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 5
tags:
  - java
related:
  - "[[Synchronization]]"
  - "[[ReentrantLock]]"
---

# Locks

## Overview
The `java.util.concurrent.locks.Lock` interface provides explicit locking with capabilities the intrinsic `synchronized` monitor lacks: non-blocking `tryLock()`, timeouts, interruptible acquisition, fairness, and multiple `Condition` wait-sets.

## Why It Matters
When you need to back off instead of blocking forever, acquire with a timeout, or coordinate multiple conditions, explicit locks are the tool. This is a common "how would you avoid a deadlock" follow-up.

## How It Works
```java
Lock lock = new ReentrantLock();
lock.lock();
try {
    // critical section
} finally {
    lock.unlock();   // MUST be in finally
}
```

Key methods: `lock()`, `unlock()`, `tryLock()`, `tryLock(timeout, unit)`, `lockInterruptibly()`.

## Lock Types
- **[[ReentrantLock]]** — mutual-exclusion lock, the direct `synchronized` replacement.
- **ReentrantReadWriteLock** — separate read/write locks; many concurrent readers, exclusive writer. Good for read-heavy caches.
- **StampedLock** — adds optimistic reads (Java 8+); faster but not reentrant.

## synchronized vs Lock
| | `synchronized` | `Lock` |
|--|----------------|--------|
| Release | automatic | manual (`finally`) |
| Try / timeout | no | yes |
| Interruptible | no | yes |
| Fairness | no | optional |
| Conditions | one (wait/notify) | multiple |

## Best Practices
- Always `unlock()` in a `finally`.
- Prefer `synchronized` for simple cases; use explicit locks only for their extra features.
- Use `tryLock` with a timeout to avoid indefinite blocking and break deadlock cycles.

## Interview Questions
- **Why can Lock avoid deadlock better?** `tryLock(timeout)` lets a thread give up and retry instead of waiting forever.
- **When ReadWriteLock?** Read-mostly shared data where writes are rare.

## Related Topics
- [[ReentrantLock]] · [[Synchronization]] · [[Deadlocks in Java]]

## Quick Revision
- Explicit locks add tryLock, timeout, interruptibility, fairness, multiple conditions. Always unlock in finally.
