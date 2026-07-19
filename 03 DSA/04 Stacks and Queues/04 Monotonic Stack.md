---
title: Monotonic Stack
aliases:
  - Monotonic Stack
domain: DSA
module: Stacks and Queues
status: Learning
difficulty: Hard
priority: High
interview: 4
revision: Weekly
order: 4
tags:
  - dsa
related:
  - "[[Stack]]"
---

# Monotonic Stack

## Overview
A monotonic stack keeps its elements in sorted order (increasing or decreasing). When a new element would break the order, you pop until the invariant holds — and each pop resolves an answer. It solves "next/previous greater/smaller element" families in O(n).

## Why It Matters
It's the pattern behind next-greater-element, daily temperatures, stock span, largest rectangle in histogram, and trapping rain water. Recognizing it turns O(n²) brute force into O(n).

## Next Greater Element
```java
// For each element, find the next greater to its right: O(n)
int[] res = new int[n];
Arrays.fill(res, -1);
Deque<Integer> stack = new ArrayDeque<>();   // indices, values decreasing
for (int i = 0; i < n; i++) {
    while (!stack.isEmpty() && a[stack.peek()] < a[i])
        res[stack.pop()] = a[i];   // a[i] is the next greater for popped index
    stack.push(i);
}
```

## Why O(n)
Each index is pushed once and popped at most once, so total work is linear despite the inner while loop.

## When To Use
- "Next/previous greater or smaller element."
- Daily temperatures, stock span.
- Largest rectangle in histogram, maximal rectangle.
- Trapping rain water (or two pointers).

## Choosing Direction
- **Decreasing stack** -> next greater element.
- **Increasing stack** -> next smaller element.
- Iterate right-to-left for "next" or left-to-right for "previous," depending on formulation.

## Interview Questions
- **What is a monotonic stack?** A stack maintaining increasing/decreasing order; pops resolve next/previous greater/smaller queries.
- **Why is it O(n)?** Each element is pushed and popped at most once.
- **Largest rectangle in histogram?** Monotonic increasing stack of bar indices; on a pop, compute area with the popped height as the limiting bar.

## Related Topics
- [[Stack]] · [[Deque]] · [[Arrays]]

## Quick Revision
- Stack kept monotonic; pop-on-violation resolves answers. Solves next/prev greater/smaller, histogram, rain water in O(n) (each index pushed/popped once). Decreasing->next greater.
