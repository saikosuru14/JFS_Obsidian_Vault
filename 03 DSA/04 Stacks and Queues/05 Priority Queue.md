---
title: Priority Queue
aliases:
  - Priority Queue
  - PriorityQueue
domain: DSA
module: Stacks and Queues
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 5
tags:
  - dsa
related:
  - "[[Queue]]"
  - "[[Heap]]"
---

# Priority Queue

## Overview
A priority queue is an abstract data type where elements are dequeued by **priority** rather than arrival order. It's almost always backed by a **[[Heap|binary heap]]**, giving O(1) peek of the min/max and O(log n) insert/extract. Java provides `java.util.PriorityQueue` (a min-heap by default).

## Why It Matters
It's the go-to structure for "top-k," "kth largest/smallest," "merge k sorted," scheduling, and greedy algorithms like Dijkstra. This note focuses on the **ADT and problem patterns**; see [[Heap]] for the underlying tree structure and internals.

## Java Usage
```java
PriorityQueue<Integer> min = new PriorityQueue<>();                    // min-heap
PriorityQueue<Integer> max = new PriorityQueue<>(Collections.reverseOrder());
PriorityQueue<int[]> byDist = new PriorityQueue<>((a, b) -> a[1] - b[1]); // custom

min.offer(x);        // insert  - O(log n)
int top = min.peek(); // min/max - O(1)
int val = min.poll(); // remove top - O(log n)
```
`PriorityQueue` is **not** sorted when iterated — only `poll()` order reflects priority.

## Problem Patterns
| Pattern | Heap setup |
|---------|-----------|
| **Kth largest** | min-heap of size k -> O(n log k) |
| **Kth smallest** | max-heap of size k |
| **Top-K frequent** | count, then size-k heap |
| **Merge K sorted lists** | min-heap of the k current heads |
| **Median of a data stream** | max-heap (low half) + min-heap (high half) |
| **Dijkstra / Prim** | min-heap keyed by distance/weight |
| **Task scheduling** | heap by deadline/priority |

## Two-Heaps (streaming median)
Keep a max-heap for the lower half and a min-heap for the upper half, balanced in size; the median is a heap top (or the average of both tops).

## Interview Questions
- **What backs a priority queue?** A binary heap -> O(1) peek, O(log n) insert/extract.
- **Kth largest with a heap?** Maintain a min-heap of size k; its top is the kth largest -> O(n log k).
- **Is Java's PriorityQueue sorted on iteration?** No — only `poll()` yields priority order.
- **Median of a stream?** Two heaps (max-heap low half, min-heap high half), kept balanced.

## Related Topics
- [[Heap]] · [[Queue]] · [[Shortest Path]] · [[Frequency Counting Pattern]]

## Quick Revision
- ADT: dequeue by priority, backed by a heap (peek O(1), insert/poll O(log n)). Java `PriorityQueue` (min by default, not sorted on iteration). Patterns: top-k (size-k heap), merge-k, two-heaps median, Dijkstra.
