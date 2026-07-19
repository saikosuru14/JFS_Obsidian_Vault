---
title: Tree Traversals
aliases:
  - Tree Traversals
domain: DSA
module: Trees
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Binary Tree]]"
---

# Tree Traversals

## Overview
Traversal = visiting every node in a defined order. **DFS** variants (inorder, preorder, postorder) go deep first; **BFS** (level-order) goes wide. Each order suits different problems.

## Why It Matters
Choosing the right traversal is half the solution. Inorder on a BST yields sorted order; level-order answers "by depth" questions; postorder builds results from children up.

## DFS Orders
```java
void inorder(TreeNode n)  { if(n==null) return; inorder(n.left); visit(n); inorder(n.right); }   // L, N, R
void preorder(TreeNode n) { if(n==null) return; visit(n); preorder(n.left); preorder(n.right); } // N, L, R
void postorder(TreeNode n){ if(n==null) return; postorder(n.left); postorder(n.right); visit(n);}// L, R, N
```
- **Inorder** — sorted order for a [[Binary Search Tree|BST]].
- **Preorder** — copy/serialize a tree (root first).
- **Postorder** — delete/free, or compute from children (height, sums).

## BFS (Level-Order)
```java
Queue<TreeNode> q = new ArrayDeque<>();
q.offer(root);
while (!q.isEmpty()) {
    int size = q.size();               // one level at a time
    for (int i = 0; i < size; i++) {
        TreeNode n = q.poll();
        visit(n);
        if (n.left != null)  q.offer(n.left);
        if (n.right != null) q.offer(n.right);
    }
}
```

## Iterative DFS
Use an explicit [[Stack]] to avoid recursion (e.g., Morris traversal achieves O(1) space for inorder).

## Interview Questions
- **Which traversal gives sorted BST output?** Inorder.
- **Which for serialization?** Preorder (root-first) reconstructs easily.
- **DFS vs BFS for trees?** DFS (recursion/stack) O(h) space; BFS (queue) O(width) space, good for level problems.

## Related Topics
- [[Binary Tree]] · [[Binary Search Tree]] · [[BFS]] · [[DFS]] · [[Stack]]

## Quick Revision
- DFS: inorder (L,N,R -> sorted BST), preorder (N,L,R -> serialize), postorder (L,R,N -> compute from children). BFS: level-order via queue (process level by level).
