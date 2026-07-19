---
title: Heap Memory
aliases:
  - Heap Memory
domain: Java
module: Memory Management
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - java
related:
  - "[[Memory Management Index|Memory Management]]"
  - "[[Young Generation]]"
  - "[[Old Generation]]"
---

# Heap Memory

## Overview
The heap is the shared runtime area where all objects and arrays live. It is managed by the garbage collector and, in HotSpot's generational collectors, split into a **Young Generation** and an **Old Generation**. This note is the sub-hub for heap layout.

## Why It Matters
Heap sizing and generation behavior drive GC frequency, pause times, and `OutOfMemoryError`s — the memory topics that show up most in production incidents.

## Generational Layout
```
Heap
├── Young Generation   (short-lived objects; Minor GC)
│    ├── Eden
│    ├── Survivor 0
│    └── Survivor 1
└── Old / Tenured      (long-lived objects; Major GC)
```
Most objects die young — the **weak generational hypothesis** — so collecting the small Young Gen frequently is cheap and reclaims most garbage. Survivors are promoted to Old Gen after enough Minor GCs.

## Key Flags
- `-Xms` / `-Xmx` — initial / max heap (set equal in servers to avoid resize pauses).
- `-Xmn` — Young Gen size.
- `-XX:+HeapDumpOnOutOfMemoryError` — capture a dump for analysis.

## Common Errors
- `OutOfMemoryError: Java heap space` — genuine growth, undersized heap, or a [[Memory Leaks in Java|leak]].
- `OutOfMemoryError: GC overhead limit exceeded` — GC runs constantly reclaiming almost nothing.

## Interview Questions
- **Heap vs stack?** Heap = shared objects, GC-managed; stack = per-thread frames/locals.
- **Why generational?** Most objects die young; collecting a small Young Gen often is far cheaper than scanning the whole heap.
- **Why are objects on the heap, not the stack?** They can outlive the method and be shared across threads (unless escape analysis proves otherwise).

## Related Topics
- [[Young Generation]] · [[Old Generation]] · [[Garbage Collection Overview]] · [[Stack Memory]]

## Quick Revision
- Shared, GC-managed object store. Young (Eden + 2 Survivors) + Old. Weak generational hypothesis: most objects die young. -Xmx sets the cap.
