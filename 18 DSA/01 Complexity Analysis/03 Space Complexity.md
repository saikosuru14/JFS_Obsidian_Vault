---
title: Space Complexity
aliases:
  - Space Complexity
domain: DSA
module: Complexity Analysis
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[Big O Notation]]"
  - "[[Time Complexity]]"
---

# Space Complexity

## Overview
Space complexity measures the **extra** memory an algorithm uses as a function of input size — auxiliary space beyond the input itself, expressed in [[Big O Notation]].

## Why It Matters
Interviews often ask for the time/space trade-off. A hashing solution may cut time from O(n²) to O(n) at the cost of O(n) space — you must justify it.

## What Counts
- **Auxiliary space** — extra structures you allocate (arrays, maps, sets).
- **Recursion stack** — each recursive call adds a frame; depth d -> O(d) space (easy to forget!).
- Usually the **input** is not counted unless the question says total space.

```java
// O(n) space: hash set of seen values
Set<Integer> seen = new HashSet<>();

// O(h) space from recursion: tree of height h
int depth(TreeNode n) {
    if (n == null) return 0;
    return 1 + Math.max(depth(n.left), depth(n.right)); // call stack up to h
}
```

## Common Time/Space Trade-offs
- Hashing/memoization: spend O(n) memory to save time.
- In-place algorithms: O(1) extra space (e.g., reverse array, quicksort partition).
- Iterative vs recursive: iterative can remove the O(depth) stack.

## Interview Questions
- **What counts toward space complexity?** Auxiliary memory allocated, including the recursion call stack; usually not the input.
- **Recursive tree traversal space?** O(h) for the call stack (O(log n) balanced, O(n) skewed).
- **Example time/space trade-off?** Two-sum: O(n) time + O(n) space (hash) vs O(n²) time + O(1) space (brute force).

## Related Topics
- [[Time Complexity]] · [[Recursion]] · [[Hashing Index|Hashing]]

## Quick Revision
- Extra memory vs n: auxiliary structures + recursion stack (O(depth)). Input usually excluded. Trade space for time via hashing/memoization; in-place = O(1).
