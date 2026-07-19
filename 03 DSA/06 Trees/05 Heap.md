---
title: Heap
aliases:
  - Heap
  - Priority Queue
  - Binary Heap
domain: DSA
module: Trees
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 5
tags:
  - dsa
related:
  - "[[Trees Index|Trees]]"
---

# Heap (Priority Queue)

## Overview
A binary heap is a **complete binary tree** stored in an array, satisfying the heap property: in a **min-heap**, every parent ≤ its children (max-heap is the reverse). It gives O(1) access to the min/max and O(log n) insert/extract. Java's `PriorityQueue` is a min-heap.

## Why It Matters
Heaps are the answer to "top-k," "kth largest/smallest," "merge k sorted," and streaming-median problems, and they back Dijkstra's shortest path.

## Array Representation
For index `i` (0-based): left child `2i+1`, right child `2i+2`, parent `(i-1)/2`. No pointers needed.

## Operations
| Operation | Complexity |
|-----------|-----------|
| peek (min/max) | O(1) |
| insert (sift up) | O(log n) |
| extract-min/max (sift down) | O(log n) |
| build-heap (heapify) | O(n) |

## Java Usage
```java
PriorityQueue<Integer> min = new PriorityQueue<>();          // min-heap
PriorityQueue<Integer> max = new PriorityQueue<>(Collections.reverseOrder());
min.offer(5); min.offer(1);
int smallest = min.poll();   // 1

// Kth largest: keep a min-heap of size k
PriorityQueue<Integer> heap = new PriorityQueue<>();
for (int x : nums) { heap.offer(x); if (heap.size() > k) heap.poll(); }
int kthLargest = heap.peek();   // O(n log k)
```

## Patterns
- **Top-k / kth largest** — size-k heap, O(n log k).
- **Merge k sorted lists** — heap of heads.
- **Median of a stream** — two heaps (max-heap low half, min-heap high half).
- **Dijkstra** — min-heap by distance.

## Interview Questions
- **Heap vs BST?** Heap: O(1) min/max, partial order, array-backed; BST: full ordering, O(log n) search, sorted traversal.
- **Kth largest efficiently?** Min-heap of size k -> O(n log k).
- **Why is build-heap O(n)?** Sift-down cost sums to O(n) (most nodes are near the bottom).

## Related Topics
- [[Heap Sort]] · [[Shortest Path]] · [[Queue]] · [[Binary Tree]]

## Quick Revision
- Complete tree in an array; min/max at root O(1), insert/extract O(log n), build O(n). Java `PriorityQueue` (min). Patterns: top-k (size-k heap), merge-k, streaming median (two heaps), Dijkstra.
