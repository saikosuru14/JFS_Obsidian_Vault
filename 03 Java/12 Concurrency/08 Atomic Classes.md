---
title: Atomic Classes
aliases:
  - Atomic Classes
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 8
tags:
  - java
related:
  - "[[Synchronization]]"
  - "[[volatile]]"
---

# Atomic Classes

## Overview
Classes in `java.util.concurrent.atomic` (`AtomicInteger`, `AtomicLong`, `AtomicReference`, `AtomicBoolean`) provide lock-free, thread-safe single-variable updates using hardware **Compare-And-Swap (CAS)**.

## Why It Matters
For counters and single-reference state, atomics are faster than locks under contention and can't deadlock. They are the correct fix for the `count++` race.

## How CAS Works
CAS is one atomic CPU instruction: "if the value is still `expected`, set it to `new`, else fail." Atomic classes loop until the swap succeeds:

```java
AtomicInteger c = new AtomicInteger();
c.incrementAndGet();                 // atomic ++
c.updateAndGet(x -> x * 2);          // atomic function
c.compareAndSet(10, 20);             // CAS: 10 -> 20 only if currently 10
```

The value is `volatile` internally, so reads are also visible.

## When Atomics Aren't Enough
- Multiple variables must change together -> use a lock.
- Very high contention -> CAS retries waste CPU; `LongAdder` (striped counters) scales better for hot counters.

## ABA Problem
A value can change A -> B -> A between reads, and CAS won't notice. `AtomicStampedReference` adds a version stamp to detect it.

## Interview Questions
- **How is AtomicInteger thread-safe without locks?** Via CAS retry loops on a volatile field — optimistic, lock-free.
- **AtomicInteger vs synchronized counter?** Atomic is lock-free and usually faster under moderate contention; synchronized blocks. For extreme contention prefer `LongAdder`.
- **What is the ABA problem?** CAS sees the same value and assumes no change though it changed and reverted; fix with a stamped reference.

## Related Topics
- [[volatile]] · [[Synchronization]] · [[Race Conditions]]

## Quick Revision
- Lock-free single-variable updates via CAS on a volatile field. Great for counters/refs. LongAdder for hot counters; watch for ABA.
