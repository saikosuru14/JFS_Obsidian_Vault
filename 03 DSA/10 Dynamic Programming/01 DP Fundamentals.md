---
title: DP Fundamentals
aliases:
  - DP Fundamentals
domain: DSA
module: Dynamic Programming
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Dynamic Programming Index|Dynamic Programming]]"
  - "[[Memoization vs Tabulation]]"
  - "[[Common DP Patterns]]"
---

# DP Fundamentals

## Overview
DP applies when a problem has **overlapping subproblems** (the same subproblem recurs) and **optimal substructure** (an optimal solution is built from optimal sub-solutions). You solve each subproblem once and reuse the result.

## Why It Matters
DP turns exponential brute-force recursions (e.g., naive Fibonacci O(2ⁿ)) into polynomial time. It's the toughest interview category, so a repeatable method matters more than memorizing solutions.

## When To Use DP
- Overlapping subproblems (a recursion tree recomputes the same states).
- Optimal substructure (combine sub-answers into the whole answer).
- Asks for count / min / max / "is it possible" over choices.
- Contrast with [[Greedy Approach|greedy]] (local choice works) and [[Divide and Conquer]] (independent subproblems).

## A Repeatable Method
1. **Define the state** — what parameters uniquely identify a subproblem? (e.g., `dp[i]` = best using first i items).
2. **Recurrence** — express `dp[state]` from smaller states.
3. **Base cases** — smallest states.
4. **Order** — compute dependencies first (or memoize top-down).
5. **Answer** — which state holds the result; optimize space if possible.

## Example: Fibonacci
```java
// O(n) time, O(1) space bottom-up
int fib(int n) {
    if (n < 2) return n;
    int a = 0, b = 1;
    for (int i = 2; i <= n; i++) { int c = a + b; a = b; b = c; }
    return b;
}
```

## Interview Questions
- **Two conditions for DP?** Overlapping subproblems and optimal substructure.
- **DP vs divide & conquer?** DP subproblems overlap (cache them); D&C subproblems are independent.
- **How do you approach a DP problem?** Define state -> recurrence -> base cases -> evaluation order -> answer (then optimize space).

## Related Topics
- [[Memoization vs Tabulation]] · [[Common DP Patterns]] · [[Recursion]] · [[Greedy vs DP]]

## Quick Revision
- Overlapping subproblems + optimal substructure. Method: state -> recurrence -> base -> order -> answer. Beats exponential recursion. Not greedy (global) and not plain D&C (independent).
