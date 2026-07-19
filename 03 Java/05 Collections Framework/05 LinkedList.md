---
title: LinkedList
aliases:
  - LinkedList
domain: Java
module: Collections Framework
status: Not Started
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 5
tags:
  - java
  - collections
related:
  - "[[List]]"
  - "[[ArrayList]]"
---

# LinkedList

## Overview
Doubly linked list implementing `List` and `Deque`. Useful as a queue/deque; rarely the right `List` in practice.

## Internal Working
- Each node holds `prev`, `item`, `next`; the list keeps `first`/`last` references.
- Add/remove at ends: O(1). Add/remove at a known node: O(1). Access by index: O(n).
- No random access — `get(i)` walks from the nearest end.

## Performance
- Higher per-element memory (two references + object header per node).
- Poor cache locality → iteration and access are slower than `ArrayList` even when Big-O looks equal.

## When to Use
- As a `Deque`/queue with frequent head/tail operations (though `ArrayDeque` is usually better).
- Almost never purely for `List` behavior.

## Common Mistakes
- Choosing it for "fast inserts" — finding the position is O(n), and cache misses dominate.

## Interview Questions
- Why is `LinkedList` rarely faster than `ArrayList`?
- Access cost by index? (O(n))
- `LinkedList` vs `ArrayDeque` for a queue?

## Related Topics
- [[List]] · [[ArrayList]]

## Quick Revision
- Doubly linked, O(1) ends, O(n) index access, cache-unfriendly. Prefer ArrayDeque for queues; rarely pick over ArrayList.
