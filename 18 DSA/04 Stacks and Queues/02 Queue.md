---
title: Queue
aliases:
  - Queue
domain: DSA
module: Stacks and Queues
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Stacks and Queues Index|Stacks and Queues]]"
  - "[[Deque]]"
---

# Queue

## Overview
A queue is a FIFO (first-in, first-out) structure: enqueue at the rear, dequeue from the front, both O(1). It preserves arrival order.

## Why It Matters
Queues drive **BFS**, level-order tree traversal, task scheduling, producer/consumer buffers, and rate limiting. "Process in arrival order / level by level" signals a queue.

## Java Usage
```java
Queue<Integer> q = new ArrayDeque<>();   // or LinkedList
q.offer(1);        // enqueue (preferred over add - no exception)
int front = q.peek();
int val = q.poll(); // dequeue (null if empty, vs remove() which throws)
```
Use `offer/poll/peek` (return null/false) over `add/remove/element` (throw) unless you want exceptions.

## Variants
- **[[Deque]]** — insert/remove at both ends (`ArrayDeque`).
- **[[Heap|PriorityQueue]]** — ordered by priority, not arrival (a heap).
- **Circular queue** — fixed-size ring buffer.
- **BlockingQueue** — thread-safe producer/consumer ([[Concurrency Index|concurrency]]).

## BFS Skeleton
```java
Queue<Node> q = new ArrayDeque<>();
q.offer(start); visited.add(start);
while (!q.isEmpty()) {
    Node n = q.poll();
    for (Node nb : n.neighbors)
        if (visited.add(nb)) q.offer(nb);   // add returns false if present
}
```

## Interview Questions
- **Stack vs queue?** LIFO vs FIFO.
- **Which Java class for a queue?** `ArrayDeque` (or `LinkedList`); `PriorityQueue` for priority order.
- **offer/poll vs add/remove?** The former return null/false on failure; the latter throw.

## Related Topics
- [[Deque]] · [[Heap]] · [[BFS]] · [[Stack]]

## Quick Revision
- FIFO, O(1) enqueue/dequeue. Use `ArrayDeque` + offer/poll/peek. Powers BFS and scheduling. Variants: deque, priority queue, circular, blocking.
