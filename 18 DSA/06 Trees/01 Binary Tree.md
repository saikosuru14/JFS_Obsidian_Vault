---
title: Binary Tree
aliases:
  - Binary Tree
domain: DSA
module: Trees
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Trees Index|Trees]]"
  - "[[Tree Traversals]]"
  - "[[Binary Search Tree]]"
---

# Binary Tree

## Overview
A binary tree is a tree where each node has at most two children (left, right). It's the base for BSTs, heaps, and expression trees. Most problems are solved by recursion over the two subtrees.

## Why It Matters
Binary-tree recursion (height, diameter, LCA, path sums) is a huge interview category, and the mental model — "solve for children, combine" — transfers everywhere.

## Node & Recursion Template
```java
class TreeNode { int val; TreeNode left, right; }

int height(TreeNode n) {
    if (n == null) return 0;
    return 1 + Math.max(height(n.left), height(n.right));
}
```

## Types
- **Full** — every node has 0 or 2 children.
- **Complete** — all levels full except possibly the last, filled left-to-right (heaps).
- **Perfect** — all internal nodes have 2 children, all leaves at the same level.
- **Balanced** — height O(log n); see [[Balanced Trees]].
- **Degenerate** — skewed to a linked list, height O(n).

## Complexity
- Traversal: O(n) time, O(h) space (recursion stack); h = log n balanced, n skewed.

## Common Problems
- Height, diameter, balanced check.
- Lowest common ancestor (LCA).
- Path sum, max path sum.
- Level-order / zigzag, invert tree, serialize/deserialize.

## Interview Questions
- **Complete vs full vs perfect?** Complete: filled left-to-right; full: 0 or 2 children; perfect: full + all leaves same level.
- **Traversal space complexity?** O(h) call stack — O(log n) balanced, O(n) skewed.
- **General approach to tree problems?** Recurse on left/right, combine results (post-order is common).

## Related Topics
- [[Tree Traversals]] · [[Binary Search Tree]] · [[Heap]] · [[Recursion]]

## Quick Revision
- ≤2 children; solve via recursion (solve children, combine). Types: full/complete/perfect/balanced/degenerate. Traversal O(n) time, O(h) space.
