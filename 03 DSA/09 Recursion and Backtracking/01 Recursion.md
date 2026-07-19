---
title: Recursion
aliases:
  - Recursion
domain: DSA
module: Recursion and Backtracking
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Recursion and Backtracking Index|Recursion and Backtracking]]"
  - "[[Backtracking]]"
  - "[[Divide and Conquer]]"
---

# Recursion

## Overview
Recursion is a function calling itself on a smaller input until it reaches a **base case**. Every recursive solution needs a base case (to stop) and a recursive case that moves toward it. Calls stack on the JVM call stack.

## Why It Matters
It's the natural way to express tree/graph traversal, divide-and-conquer, and backtracking, and the foundation for dynamic programming (recursion + memoization).

## Anatomy
```java
long factorial(int n) {
    if (n <= 1) return 1;          // base case
    return n * factorial(n - 1);   // recursive case (toward base)
}
```
Each call adds a stack frame; depth d -> O(d) space. Missing/incorrect base case -> `StackOverflowError`.

## Recursion vs Iteration
- Recursion: cleaner for tree-shaped problems; O(depth) stack overhead.
- Iteration: no stack overhead; sometimes clearer for linear problems.
- Any recursion can be converted to iteration with an explicit [[Stack|stack]].

## Recursion Tree & Cost
Model calls as a tree; total work = sum over nodes. Fibonacci naively branches into O(2ⁿ) calls (recomputing subproblems) — the motivation for [[Dynamic Programming Index|memoization]].

## Common Mistakes
- No/incorrect base case -> infinite recursion (stack overflow).
- Not reducing the problem each call.
- Deep recursion on large inputs (prefer iteration or increase stack).

## Interview Questions
- **Two required parts of recursion?** Base case and a recursive case that progresses toward it.
- **Recursion vs iteration trade-off?** Clarity for tree problems vs O(depth) stack cost; convertible via an explicit stack.
- **Why is naive Fibonacci O(2ⁿ)?** Overlapping subproblems recomputed — fix with memoization ([[Dynamic Programming]]).

## Related Topics
- [[Backtracking]] · [[Divide and Conquer]] · [[Dynamic Programming Index|Dynamic Programming]] · [[Tree Traversals]]

## Quick Revision
- Base case + shrink toward it; uses O(depth) stack. Great for trees/D&C/backtracking. Overlapping subproblems -> memoize. Convertible to iteration with a stack.
