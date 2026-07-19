---
title: Memoization vs Tabulation
aliases:
  - Memoization vs Tabulation
  - Memoization
  - Tabulation
domain: DSA
module: Dynamic Programming
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[DP Fundamentals]]"
---

# Memoization vs Tabulation

## Overview
The two ways to implement DP. **Memoization** is top-down: recurse naturally and cache results. **Tabulation** is bottom-up: fill a table iteratively from base cases. Both give the same complexity; they differ in style and constants.

## Why It Matters
Interviewers often ask you to convert a recursion to memoized DP, then optimize to tabulation with reduced space. Knowing both, and when each is cleaner, is expected.

## Memoization (Top-Down)
```java
Integer[] memo;
int rob(int[] a, int i) {
    if (i < 0) return 0;
    if (memo[i] != null) return memo[i];
    return memo[i] = Math.max(rob(a, i - 1), a[i] + rob(a, i - 2));
}
```
- Write the recurrence, add a cache; only computes needed states.
- Uses recursion stack (O(depth)); risk of stack overflow for deep states.

## Tabulation (Bottom-Up)
```java
int rob(int[] a) {
    int n = a.length, prev2 = 0, prev1 = 0;
    for (int i = 0; i < n; i++) {
        int cur = Math.max(prev1, a[i] + prev2);
        prev2 = prev1; prev1 = cur;
    }
    return prev1;   // O(n) time, O(1) space
}
```
- Iterative; no stack overhead; often enables **space optimization** (keep only the last row/two values).

## Comparison
| | Memoization | Tabulation |
|--|-------------|------------|
| Direction | top-down | bottom-up |
| Structure | recursion + cache | loop + table |
| Computes | only needed states | all states |
| Space | O(states) + stack | O(states), often reducible |
| Ease | closer to the recurrence | needs explicit order |

## Interview Questions
- **Memoization vs tabulation?** Top-down recursion+cache vs bottom-up iterative table; same complexity.
- **When prefer tabulation?** To avoid deep recursion / stack overflow and to enable space optimization.
- **When prefer memoization?** When the recurrence is natural and not all states are needed.

## Related Topics
- [[DP Fundamentals]] · [[Common DP Patterns]] · [[Recursion]]

## Quick Revision
- Memo = top-down recursion + cache (only needed states, uses stack). Tab = bottom-up table (all states, no stack, space-optimizable). Same big-O; pick by clarity/stack/space.
