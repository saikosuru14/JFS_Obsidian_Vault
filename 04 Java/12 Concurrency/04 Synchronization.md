---
title: Synchronization
aliases:
  - Synchronization
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 4
tags:
  - java
related:
  - "[[Concurrency Index|Concurrency]]"
  - "[[volatile]]"
  - "[[Locks]]"
  - "[[Atomic Classes]]"
  - "[[Deadlocks in Java]]"
---

# Synchronization

## Overview
`synchronized` provides **mutual exclusion** (one thread in the critical section at a time) and **visibility** (a happens-before edge on monitor unlock → next lock). It is the built-in, intrinsic-lock solution to shared mutable state. This note is the sub-hub for coordination tools.

## Why It Matters
It is the simplest correct fix for compound actions and the baseline every interview compares locks and atomics against.

## How It Works
Every object has an intrinsic monitor. Entering a `synchronized` block acquires it; exiting releases it and flushes changes to main memory.

```java
synchronized void inc() { count++; }              // locks 'this'
void inc() { synchronized (lock) { count++; } }   // locks a private final lock (preferred)
static synchronized void m() { }                  // locks the Class object
```

Prefer a **private final lock object** over `synchronized(this)` so external code can't accidentally lock on your instance.

## Visibility + happens-before
Unlocking a monitor happens-before the next lock on the same monitor, so writes inside the block are visible to the next holder. See [[Java Memory Model]].

## Best Practices
- Keep critical sections small; never do I/O or call unknown code while holding a lock.
- Lock on a private, dedicated object.
- Reach for [[Atomic Classes]] for single variables and [[Locks]]/[[ReentrantLock]] when you need `tryLock`, timeouts, or fairness.

## Common Mistakes
- Synchronizing getters but not setters (or on different monitors).
- Holding a lock across a blocking call, inviting [[Deadlocks in Java|deadlock]].

## Interview Questions
- **What two guarantees does `synchronized` give?** Mutual exclusion and visibility (happens-before).
- **`synchronized` method vs block?** The method locks the whole invocation on `this`/Class; a block narrows the scope and lets you pick the monitor.
- **`synchronized` vs `ReentrantLock`?** Lock adds `tryLock`, interruptible/timed acquisition, fairness, and multiple conditions — at the cost of manual `unlock()`.

## Related Topics
- [[volatile]] · [[Locks]] · [[Atomic Classes]] · [[Deadlocks in Java]] · [[Race Conditions]]

## Quick Revision
- `synchronized` = mutual exclusion + visibility via intrinsic monitor. Lock on a private object, keep sections tiny, no blocking calls inside.
