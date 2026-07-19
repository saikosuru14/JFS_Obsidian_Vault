---
title: Doubly Linked List
aliases:
  - Doubly Linked List
domain: DSA
module: Linked Lists
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Singly Linked List]]"
---

# Doubly Linked List

## Overview
A doubly linked list gives each node both `next` and `prev` pointers, enabling O(1) traversal and deletion in both directions. Java's `LinkedList` is a doubly linked list.

## Why It Matters
The `prev` pointer makes O(1) removal of a known node possible without scanning for its predecessor — the key enabler for an **LRU cache** (doubly linked list + hash map).

## Node & Operations
```java
class Node { int val; Node prev, next; }

// Delete a known node in O(1):
node.prev.next = node.next;
if (node.next != null) node.next.prev = node.prev;
```

## Singly vs Doubly
| | Singly | Doubly |
|--|--------|--------|
| Pointers/node | 1 (next) | 2 (prev, next) |
| Backward traversal | no | yes |
| Delete known node | O(n) (find prev) | O(1) |
| Memory | less | more (extra pointer) |

## Where It's Used
- **LRU cache** — O(1) move-to-front/evict-tail with a hash map to nodes ([[LinkedHashMap]] uses this internally).
- Browser history, undo/redo, deque implementations.

## Interview Questions
- **Singly vs doubly linked list?** Doubly adds `prev` for O(1) backward traversal and O(1) deletion of a known node, at the cost of extra memory.
- **How do you build an LRU cache?** HashMap(key -> node) + doubly linked list for recency order; get/put O(1).
- **What Java class is a doubly linked list?** `java.util.LinkedList` (also a `Deque`).

## Related Topics
- [[Singly Linked List]] · [[LinkedHashMap]] · [[Deque]]

## Quick Revision
- Nodes with prev+next: O(1) bidirectional traversal and O(1) delete of a known node. Powers LRU caches and deques. More memory than singly.
