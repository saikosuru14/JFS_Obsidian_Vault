---
title: ReentrantLock
aliases:
  - ReentrantLock
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 6
tags:
  - java
related:
  - "[[Locks]]"
---

# ReentrantLock

## Overview
`ReentrantLock` is the standard explicit mutual-exclusion lock. **Reentrant** means the holding thread can re-acquire it without deadlocking; an internal hold count increments on each `lock()` and must be matched by equal `unlock()` calls.

## Why It Matters
It is the drop-in upgrade from `synchronized` when you need `tryLock`, timeouts, interruptible acquisition, fairness, or multiple conditions.

## How It Works
```java
private final ReentrantLock lock = new ReentrantLock();

public boolean transfer() {
    if (lock.tryLock(1, TimeUnit.SECONDS)) {   // give up if not free
        try { /* critical section */ return true; }
        finally { lock.unlock(); }
    }
    return false;   // backed off
}
```

## Fairness
`new ReentrantLock(true)` grants the lock in FIFO order, preventing starvation but lowering throughput. The default (unfair) is faster because it allows barging and is the right choice unless you observe starvation.

## Conditions
`lock.newCondition()` gives named wait-sets (`await()` / `signal()`), replacing `wait()`/`notify()` — you can have separate conditions like `notFull` and `notEmpty` on one lock.

## Best Practices
- Backed by AQS (AbstractQueuedSynchronizer); same engine behind `Semaphore`, `CountDownLatch`.
- Match every `lock()` with an `unlock()` in `finally`.
- Default to unfair; enable fairness only to fix measured starvation.

## Interview Questions
- **What does "reentrant" mean?** The same thread can acquire the lock it already holds; hold count tracks nesting.
- **ReentrantLock vs synchronized?** Same mutual exclusion, but adds try/timeout/interruptible/fair acquisition and multiple conditions, at the cost of manual unlock.

## Related Topics
- [[Locks]] · [[Synchronization]] · [[Deadlocks in Java]]

## Quick Revision
- Explicit reentrant lock (hold count). tryLock/timeout/fair/conditions. Unlock in finally. Default unfair.
