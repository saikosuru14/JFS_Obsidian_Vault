---
title: volatile
aliases:
  - volatile
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 7
tags:
  - java
related:
  - "[[Synchronization]]"
  - "[[Atomic Classes]]"
---

# volatile

## Overview
`volatile` guarantees **visibility** and **ordering** for a single field: reads and writes go to main memory, and the JMM forbids reordering across a volatile access. It does **not** provide atomicity for compound operations.

## Why It Matters
It is the cheapest correct way to publish a flag or a reference between threads without a lock. Misusing it for counters is a very common bug and interview trap.

## How It Works
A volatile write happens-before every subsequent volatile read of the same field. This creates a memory barrier: writes made before the volatile write become visible to a thread that reads it.

```java
private volatile boolean running = true;   // correct: single-writer flag
public void stop() { running = false; }
public void run() { while (running) { /* work */ } }
```

## What It Does NOT Fix
```java
private volatile int count = 0;
count++;   // STILL broken: read-modify-write is not atomic
```
Use [[Atomic Classes|AtomicInteger]] or [[Synchronization]] for compound updates.

## Common Uses
- Stop/status flags (single writer, many readers).
- Safe publication of an immutable object reference.
- The double-checked locking idiom (the field must be volatile).

## Interview Questions
- **volatile vs synchronized?** volatile gives visibility/ordering for one field with no mutual exclusion; synchronized gives both plus atomicity for a block.
- **Does volatile make `count++` safe?** No — increment is three ops; volatile only guarantees each individual read/write is visible.
- **When is volatile enough?** When one thread writes and others only read, or writes don't depend on the current value.

## Related Topics
- [[Atomic Classes]] · [[Synchronization]] · [[Java Memory Model]]

## Quick Revision
- Visibility + ordering for one field, no atomicity. Great for flags; useless for counters.
