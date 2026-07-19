---
title: Fast and Slow Pointers
aliases:
  - Fast and Slow Pointers
  - Floyd's Cycle Detection
domain: DSA
module: Linked Lists
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[Linked Lists Index|Linked Lists]]"
  - "[[Reversal and Cycle Detection]]"
---

# Fast and Slow Pointers

## Overview
The fast/slow (tortoise and hare) technique advances two pointers at different speeds — typically slow by 1 and fast by 2. It finds the middle, detects cycles, and locates cycle starts in O(n) time and O(1) space.

## Why It Matters
It's the canonical O(1)-space answer to "detect a cycle" and "find the middle," both extremely common. Beats the naive hash-set approach on space.

## Find The Middle
```java
ListNode slow = head, fast = head;
while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}
return slow;   // middle (second middle for even length)
```

## Detect A Cycle (Floyd's)
```java
ListNode slow = head, fast = head;
while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow == fast) return true;   // they meet inside the loop
}
return false;
```
If there's a cycle, the fast pointer laps the slow one and they meet. To find the **cycle start**, reset one pointer to head and advance both by 1 until they meet again.

## When To Use
- Cycle detection / find cycle start (linked list or functional graph).
- Middle of a list, palindrome check (find middle + reverse half).
- Nth-from-end (spaced pointers).

## Interview Questions
- **How detect a cycle in O(1) space?** Floyd's fast/slow — if they meet, there's a cycle.
- **Why do they meet?** Fast gains one step per iteration on slow inside the loop, so it eventually catches up.
- **Find the cycle's start?** After meeting, move one pointer to head; advance both by 1; they meet at the start.

## Related Topics
- [[Reversal and Cycle Detection]] · [[Two Pointers]] · [[Singly Linked List]]

## Quick Revision
- Slow +1, fast +2. Meeting => cycle; midpoint when fast hits the end. Cycle start: reset one to head, step both by 1. O(n) time, O(1) space.
