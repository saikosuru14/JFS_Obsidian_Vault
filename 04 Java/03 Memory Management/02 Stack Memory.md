---
title: Stack Memory
aliases:
  - Stack Memory
domain: Java
module: Memory Management
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 2
tags:
  - java
related:
  - "[[Memory Management Index|Memory Management]]"
  - "[[Heap Memory]]"
---

# Stack Memory

## Overview
Each thread has its own JVM stack, made of **stack frames** — one per method call. A frame holds local variables, operand stack, and the return address. Frames are pushed on call and popped on return, so allocation is trivially fast (just move a pointer).

## Why It Matters
Stack confinement is the cheapest form of thread safety: because each thread has a private stack, local variables and method parameters can never be shared, so they need no synchronization.

## What Lives Here
- Local primitive values.
- **References** to heap objects (the object itself is on the [[Heap Memory|heap]]; only the pointer is on the stack).
- Method parameters and return addresses.

## Stack vs Heap
| | Stack | Heap |
|--|-------|------|
| Scope | per-thread | shared |
| Stores | frames, locals, refs | objects, arrays |
| Lifetime | method call | until unreachable (GC) |
| Speed | very fast (LIFO) | slower (allocation + GC) |
| Error | `StackOverflowError` | `OutOfMemoryError` |

## Common Mistakes / Errors
- **`StackOverflowError`** — deep or infinite recursion; tune with `-Xss` only as a stopgap.
- Assuming a large local array is "on the stack" — the reference is, the array is on the heap.

## Interview Questions
- **Why are local variables thread-safe?** Each thread has its own stack; locals are never shared (stack confinement).
- **What causes StackOverflowError vs OutOfMemoryError?** Too-deep call chains vs heap exhaustion.
- **Where is a local object stored?** Reference on the stack, object on the heap (barring escape-analysis stack allocation).

## Related Topics
- [[Heap Memory]] · [[Java Memory Model]] · [[Threads]]

## Quick Revision
- Per-thread frames (locals, refs, return addr). Fast LIFO, auto-freed on return. Locals are thread-safe by confinement. Deep recursion -> StackOverflowError.
