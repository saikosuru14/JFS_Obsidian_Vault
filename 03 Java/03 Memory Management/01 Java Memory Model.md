---
title: Java Memory Model
aliases:
  - Java Memory Model
domain: Java
module: Memory Management
status: Learning
difficulty: Hard
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
related:
  - "[[Memory Management Index|Memory Management]]"
  - "[[volatile]]"
  - "[[Synchronization]]"
---

# Java Memory Model (JMM)

## Overview
The JMM is the spec that defines **when** a write by one thread becomes visible to a read by another, and **what reorderings** the compiler/CPU may perform. It's the contract that makes multithreaded programs reason-able despite caches and out-of-order execution.

## Why It Matters
Without the JMM's guarantees, a thread could see stale values or partially constructed objects. Every concurrency primitive (`volatile`, `synchronized`, atomics, locks) is defined in terms of it.

## Key Concepts
- **Main memory vs working memory** — threads may cache values in registers/CPU caches; the JMM says when they must reconcile with main memory.
- **Atomicity** — reads/writes of most primitives are atomic; `long`/`double` are only guaranteed atomic when `volatile`.
- **Visibility** — a write is visible to another thread only if a happens-before edge connects them.
- **Ordering** — instructions may be reordered unless a happens-before relationship forbids it.

## Happens-Before (the core rule)
If action A happens-before action B, A's effects are visible to B. Key edges:
- Program order within a single thread.
- `volatile` write -> subsequent `volatile` read of the same field.
- `synchronized` unlock -> next lock on the same monitor.
- `Thread.start()` -> the started thread's actions.
- A thread's actions -> another thread's successful `join()`.
- `final` field initialization -> visibility after safe construction.

## Safe Publication
Share an object only via: a `volatile`/`final` field, a value from a concurrent collection, or under a lock. Publishing via a plain field is a data race and may expose a partially built object.

## Interview Questions
- **What does happens-before guarantee?** Visibility and ordering — if A happens-before B, B sees everything A did.
- **Are `long`/`double` writes atomic?** Not guaranteed unless declared `volatile` (they may tear on 32-bit).
- **How do `final` fields help?** Correctly constructed objects with `final` fields are safely visible after publication without extra synchronization.

## Related Topics
- [[volatile]] · [[Synchronization]] · [[Heap Memory]]

## Quick Revision
- JMM = visibility + ordering rules via happens-before. volatile/synchronized/final/start/join create edges. Publish safely to avoid seeing stale or half-built objects.
