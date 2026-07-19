---
title: Reversal and Cycle Detection
aliases:
  - Reversal and Cycle Detection
  - Linked List Reversal
domain: DSA
module: Linked Lists
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 4
tags:
  - dsa
related:
  - "[[Linked Lists Index|Linked Lists]]"
  - "[[Fast and Slow Pointers]]"
---

# Reversal and Cycle Detection

## Overview
Two must-know linked-list operations: **iterative reversal** (re-point each node backward) and **cycle handling** (detect and find the start via [[Fast and Slow Pointers|Floyd's]]). Both are O(n) time, O(1) space.

## Why It Matters
Reversal is the single most-asked linked-list operation and a building block (reverse in k-groups, palindrome check). Cycle detection tests pointer discipline.

## Iterative Reversal
```java
ListNode reverse(ListNode head) {
    ListNode prev = null, cur = head;
    while (cur != null) {
        ListNode next = cur.next;   // save
        cur.next = prev;            // reverse pointer
        prev = cur;                 // advance prev
        cur = next;                 // advance cur
    }
    return prev;                    // new head
}
```
The order matters: **save next, relink, advance** — reassigning `cur.next` before saving loses the rest of the list.

## Recursive Reversal
```java
ListNode reverse(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode newHead = reverse(head.next);
    head.next.next = head;   // point the next node back to me
    head.next = null;
    return newHead;
}
```
O(n) time but O(n) stack space.

## Cycle: Detect + Find Start
Use [[Fast and Slow Pointers|Floyd's]] to detect; to find the start, after they meet reset one pointer to head and advance both by one until they meet again.

## Interview Questions
- **Reverse a linked list iteratively?** Track prev/cur/next; relink each node backward; return prev. O(n)/O(1).
- **Iterative vs recursive reversal?** Same time; iterative is O(1) space, recursive is O(n) stack.
- **Detect and locate a cycle?** Floyd's meet -> reset one to head -> step both by 1 -> meet at cycle start.

## Related Topics
- [[Fast and Slow Pointers]] · [[Singly Linked List]] · [[Two Pointers]]

## Quick Revision
- Reversal: prev/cur/next, save->relink->advance, return prev (O(1) space). Recursion is O(n) stack. Cycle: Floyd's detect + reset-to-head to find start.
