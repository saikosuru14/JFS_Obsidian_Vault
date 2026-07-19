---
title: Binary Search Tree
aliases:
  - Binary Search Tree
  - BST
domain: DSA
module: Trees
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[Binary Tree]]"
  - "[[Balanced Trees]]"
---

# Binary Search Tree (BST)

## Overview
A BST is a binary tree with the ordering invariant: for every node, all keys in the left subtree are smaller and all in the right subtree are larger. This enables O(h) search/insert/delete — O(log n) when balanced.

## Why It Matters
It's the model behind `TreeMap`/`TreeSet` and any ordered/range-query structure. The catch — degeneration to O(n) when unbalanced — motivates [[Balanced Trees]].

## Operations
```java
TreeNode search(TreeNode n, int key) {
    while (n != null && n.val != key)
        n = key < n.val ? n.left : n.right;   // go left/right by comparison
    return n;
}
```
- **Search/Insert** — compare and descend, O(h).
- **Delete** — three cases: leaf (remove), one child (splice), two children (replace with inorder successor/predecessor).
- **Inorder traversal** yields keys in **sorted order**.

## Complexity
| | Balanced | Skewed (worst) |
|--|----------|----------------|
| search/insert/delete | O(log n) | O(n) |

Inserting sorted data into a plain BST creates a degenerate (linked-list) tree — hence self-balancing variants.

## BST vs Hash Table
- BST: **ordered** — supports range queries, floor/ceiling, sorted iteration; O(log n).
- Hash: **unordered** — O(1) average, no ordering.

## Interview Questions
- **BST invariant?** Left subtree < node < right subtree, recursively.
- **Why can a BST degrade to O(n)?** Sorted inserts create a skewed (linked-list) shape; fix with self-balancing (AVL/red-black).
- **Validate a BST?** Inorder must be strictly increasing, or check min/max bounds recursively.
- **When BST over hash map?** When you need ordering: range queries, floor/ceiling, sorted traversal.

## Related Topics
- [[Balanced Trees]] · [[Tree Traversals]] · [[TreeMap]] · [[Binary Search]]

## Quick Revision
- left < node < right; O(h) ops (O(log n) balanced, O(n) skewed). Inorder = sorted. Delete: leaf/one-child/two-children(successor). Ordered alternative to hashing.
