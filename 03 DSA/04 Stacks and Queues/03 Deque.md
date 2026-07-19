---
title: Deque
aliases:
  - Deque
  - Double Ended Queue
domain: DSA
module: Stacks and Queues
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[Queue]]"
  - "[[Monotonic Stack]]"
---

# Deque (Double-Ended Queue)

## Overview
A deque supports O(1) insertion and removal at **both** ends. It generalizes both stack and queue, so `ArrayDeque` is the recommended implementation for each.

## Why It Matters
It's the backing structure for the **sliding-window maximum** (monotonic deque) and any problem needing efficient access to both ends. In Java, `ArrayDeque` is the go-to for stacks and queues alike.

## Java Usage
```java
Deque<Integer> dq = new ArrayDeque<>();
dq.offerFirst(1); dq.offerLast(2);   // add to front / back
dq.peekFirst();   dq.peekLast();
dq.pollFirst();   dq.pollLast();     // remove from front / back
```
As a stack: `push`/`pop` (front). As a queue: `offer`/`poll` (back/front).

## Sliding Window Maximum (monotonic deque)
```java
// Max of each window of size k: O(n)
Deque<Integer> dq = new ArrayDeque<>();   // stores indices, values decreasing
for (int i = 0; i < n; i++) {
    while (!dq.isEmpty() && a[dq.peekLast()] <= a[i]) dq.pollLast(); // pop smaller
    dq.offerLast(i);
    if (dq.peekFirst() <= i - k) dq.pollFirst();   // drop out-of-window
    if (i >= k - 1) result.add(a[dq.peekFirst()]); // front = window max
}
```

## Interview Questions
- **What is a deque?** A queue allowing O(1) add/remove at both ends; generalizes stack and queue.
- **Why `ArrayDeque` for stacks and queues?** Faster than `Stack`/`LinkedList`, no synchronization, cache-friendly array backing.
- **Sliding window maximum approach?** Monotonic deque of indices with decreasing values -> O(n).

## Related Topics
- [[Queue]] · [[Stack]] · [[Monotonic Stack]] · [[Sliding Window]]

## Quick Revision
- O(1) both ends; use `ArrayDeque` for stacks/queues/deques. Monotonic deque solves sliding-window maximum in O(n).
