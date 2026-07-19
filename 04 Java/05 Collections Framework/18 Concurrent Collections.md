---
title: Concurrent Collections
aliases:
  - Concurrent Collections
domain: Java
module: Collections Framework
status: Not Started
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 18
tags:
  - java
  - collections
  - concurrency
related:
  - "[[Collections Framework]]"
  - "[[ConcurrentHashMap]]"
---

# Concurrent Collections

## Overview
`java.util.concurrent` provides collections built for multithreaded access without wrapping everything in a global lock. Prefer them over `Collections.synchronizedXxx`.

## The Key Players
| Type | Use for | Notes |
|------|---------|-------|
| [[ConcurrentHashMap]] | concurrent map | Per-bin locking, lock-free reads |
| `CopyOnWriteArrayList` | read-mostly lists | Writes copy the array; great for listeners |
| `ConcurrentLinkedQueue` | non-blocking FIFO | Lock-free (CAS) |
| `BlockingQueue` (`ArrayBlockingQueue`, `LinkedBlockingQueue`) | producer/consumer | `put`/`take` block |
| `ConcurrentSkipListMap/Set` | sorted + concurrent | O(log n), NavigableMap |

## synchronized wrappers vs concurrent collections
- `Collections.synchronizedMap` locks the whole map and still needs manual locking to iterate safely.
- Concurrent collections use finer-grained or lock-free strategies and offer weakly consistent iterators (no CME).

## When to Use
- Shared state across threads: reach for these first.
- Bounded producer/consumer handoff → `BlockingQueue`.
- Read-mostly with rare writes → `CopyOnWriteArrayList`.

## Common Mistakes
- Using `CopyOnWriteArrayList` for write-heavy workloads (every write copies).
- Assuming compound operations are atomic — they aren't across calls.

## Interview Questions
- Concurrent collections vs `synchronized` wrappers?
- When is `CopyOnWriteArrayList` appropriate?
- Blocking vs non-blocking queues?

## Related Topics
- [[Collections Framework]] · [[ConcurrentHashMap]]

## Quick Revision
- Prefer j.u.c: ConcurrentHashMap, CopyOnWriteArrayList (read-mostly), BlockingQueue (producer/consumer), ConcurrentSkipList (sorted). Weakly consistent, no global lock.
