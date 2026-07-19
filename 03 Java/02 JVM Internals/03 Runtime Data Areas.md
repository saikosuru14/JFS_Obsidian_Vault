---
title: Runtime Data Areas
aliases:
  - Runtime Data Areas
domain: Java
module: JVM Internals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - java
related:
  - "[[JVM Architecture]]"
  - "[[Program Counter Register]]"
  - "[[Native Method Stack]]"
---

# Runtime Data Areas

## Overview
The runtime data areas are the memory regions the JVM creates at startup and per thread. Some are **shared** (heap, Metaspace); others are **per-thread** (JVM stack, PC register, native method stack).

## Why It Matters
Knowing which regions are shared vs per-thread explains thread safety of locals, where `OutOfMemoryError` vs `StackOverflowError` come from, and how memory tuning flags map to regions.

## The Areas
| Area | Scope | Holds | Error on exhaustion |
|------|-------|-------|---------------------|
| **[[Heap Memory\|Heap]]** | shared | objects, arrays | `OutOfMemoryError: Java heap space` |
| **[[Metaspace]]** | shared | class metadata | `OutOfMemoryError: Metaspace` |
| **JVM Stack** ([[Stack Memory]]) | per-thread | frames, locals, refs | `StackOverflowError` |
| **[[Program Counter Register\|PC Register]]** | per-thread | address of current instruction | - |
| **[[Native Method Stack]]** | per-thread | native (JNI) call frames | `StackOverflowError` |

## Shared vs Per-Thread
- **Shared** across all threads: Heap + Metaspace -> require synchronization for mutable state.
- **Per-thread**: Stack, PC register, Native method stack -> naturally isolated (stack confinement).

## Interview Questions
- **Which areas are shared vs per-thread?** Heap and Metaspace are shared; stack, PC register, native method stack are per-thread.
- **Where are local variables and objects stored?** Locals/refs on the per-thread stack; the objects themselves on the shared heap.
- **What error signals stack vs heap exhaustion?** `StackOverflowError` vs `OutOfMemoryError`.

## Related Topics
- [[Program Counter Register]] · [[Native Method Stack]] · [[Heap Memory]] · [[Stack Memory]] · [[Metaspace]]

## Quick Revision
- Shared: heap + Metaspace. Per-thread: JVM stack, PC register, native method stack. Locals on stack, objects on heap. Stack -> SOE, heap/meta -> OOM.
