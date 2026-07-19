---
title: Singly Linked List
aliases:
  - Singly Linked List
domain: DSA
module: Linked Lists
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Linked Lists Index|Linked Lists]]"
  - "[[Doubly Linked List]]"
---

# Singly Linked List

## Overview
A singly linked list is a chain of nodes, each holding a value and a `next` pointer to the following node. The list is referenced by its `head`; the last node points to `null`.

## Why It Matters
It's the base structure for pointer-manipulation problems and underpins stacks, queues, and hash-bucket chains. The dummy-head trick and careful null handling are the core skills.

## Node & Basics
```java
class ListNode { int val; ListNode next; ListNode(int v){ val = v; } }

// Traverse: O(n)
for (ListNode cur = head; cur != null; cur = cur.next) visit(cur.val);

// Insert at head: O(1)
ListNode n = new ListNode(x); n.next = head; head = n;
```

## Complexity
| Operation | Singly Linked List |
|-----------|--------------------|
| Access / search | O(n) |
| Insert/delete at head | O(1) |
| Insert/delete at tail | O(n) (no tail ptr) / O(1) (with tail) |
| Insert/delete after a known node | O(1) |

## Dummy Head Pattern
```java
ListNode dummy = new ListNode(0);
dummy.next = head;
// operate with prev starting at dummy - removes head-special-casing
return dummy.next;
```
Using a dummy (sentinel) node avoids special cases when the head itself may change (deletion, merge).

## Common Mistakes
- Losing the rest of the list by reassigning `next` before saving it.
- Null-pointer errors at head/tail boundaries.
- Forgetting to advance pointers (infinite loop).

## Interview Questions
- **Array vs linked list?** Array: O(1) index, contiguous, cache-friendly. List: O(1) insert/delete at position, O(n) access, no resizing.
- **Why a dummy head?** Eliminates edge cases when the head can change.
- **Find the nth-from-end node?** Two pointers spaced n apart (one pass).

## Related Topics
- [[Doubly Linked List]] · [[Fast and Slow Pointers]] · [[Reversal and Cycle Detection]] · [[LinkedList]]

## Quick Revision
- Node(val,next) chain from head to null. O(1) insert/delete at position, O(n) access. Use a dummy head; save `next` before relinking.
