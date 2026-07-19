---
title: ArrayList
aliases:
  - ArrayList
domain: Java
module: Collections Framework
status: Not Started
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 4
tags:
  - java
  - collections
related:
  - "[[List]]"
  - "[[LinkedList]]"
---

# ArrayList

## Overview
Resizable-array implementation of `List`. O(1) random access and cache-friendly iteration make it the default list in Java.

## Internal Working
- Backed by an `Object[]`. Default capacity 10 on first add.
- **Growth**: when full, allocates a new array ~1.5× (`oldCap + (oldCap >> 1)`) and copies elements → amortized O(1) `add`.
- `add(i, e)` / `remove(i)` shift subsequent elements → O(n).
- `get`/`set` are O(1).

## Performance
- Amortized O(1) append; O(n) middle insert/remove and `contains`.
- Presize with `new ArrayList<>(expectedSize)` for large data to avoid repeated resizes/copies.
- Cache locality makes it faster than `LinkedList` for almost all real workloads.

## Best Practices
- Presize when the count is known.
- Use `removeIf` for bulk deletes (avoids repeated shifts + CME).
- Not thread-safe — use `CopyOnWriteArrayList` or external sync for concurrency.

## Common Mistakes
- Removing in a loop by index while iterating forward (skips elements).
- Assuming `LinkedList` is faster for inserts — measure.

## Interview Questions
- How does ArrayList grow, and why is append amortized O(1)?
- Cost of `add(0, e)`? (O(n))
- ArrayList vs LinkedList vs Vector?

## Related Topics
- [[List]] · [[LinkedList]]

## Quick Revision
- Array-backed, O(1) get, amortized O(1) append (1.5× growth), O(n) middle ops. Presize for large data. Default list.
