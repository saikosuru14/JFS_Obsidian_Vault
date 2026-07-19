---
title: Queue
aliases:
  - Queue
domain: Java
module: Collections Framework
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 11
tags:
  - java
  - collections
related:
  - "[[Collections Framework]]"
---

# Queue

## Overview
`Queue` models FIFO processing; `Deque` (double-ended queue) supports both ends and stack behavior. Key implementations: `ArrayDeque`, `PriorityQueue`, `LinkedList`.

## Implementations
| Impl | Semantics | Notes |
|------|-----------|-------|
| `ArrayDeque` | FIFO/LIFO | Fast, no nulls — default deque/stack |
| `PriorityQueue` | priority order | Min-heap; O(log n) offer/poll |
| `LinkedList` | FIFO | Also a List; usually beaten by ArrayDeque |

## API Note
Prefer the exception-free methods for capacity-bound queues: `offer`/`poll`/`peek` over `add`/`remove`/`element`.

## When to Use
- Task scheduling, BFS, producer/consumer buffers.
- Priority scheduling → `PriorityQueue`.
- Blocking producer/consumer → `BlockingQueue` (see [[Concurrent Collections]]).

## Common Mistakes
- Using `Stack` (legacy) instead of `ArrayDeque` for stack behavior.
- Assuming `PriorityQueue` iteration is sorted (only `poll` order is).

## Interview Questions
- `ArrayDeque` vs `LinkedList` vs `Stack`?
- How is `PriorityQueue` implemented, and its complexity?
- `offer/poll` vs `add/remove`?

## Related Topics
- [[Collections Framework]]

## Quick Revision
- FIFO (Deque = both ends). ArrayDeque default; PriorityQueue = heap O(log n); use offer/poll; BlockingQueue for concurrency.
