---
title: Common DP Patterns
aliases:
  - Common DP Patterns
  - Knapsack
domain: DSA
module: Dynamic Programming
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[DP Fundamentals]]"
---

# Common DP Patterns

## Overview
Most DP interview problems are variations of a handful of patterns. Recognizing the pattern gives you the state and recurrence quickly.

## Why It Matters
You can't memorize every DP problem, but you can learn ~8 patterns and map new problems onto them. That recognition is the interview skill.

## The Patterns
| Pattern | State | Examples |
|---------|-------|----------|
| **Linear / 1D** | `dp[i]` from prior indices | house robber, climbing stairs, LIS |
| **0/1 Knapsack** | `dp[i][w]` take/skip item | subset sum, partition equal sum, target sum |
| **Unbounded knapsack** | reuse items | coin change, rod cutting |
| **LCS / edit distance** | `dp[i][j]` over two strings | LCS, edit distance, longest common substring |
| **Grid** | `dp[r][c]` from top/left | unique paths, min path sum |
| **Interval** | `dp[i][j]` over a range | matrix chain, burst balloons, palindrome partitioning |
| **DP on subsets (bitmask)** | `dp[mask]` | TSP, assignment |
| **DP on trees** | `dp[node][state]` | house robber III, tree diameter |

## Examples
```java
// Coin change (unbounded knapsack): min coins to make amount
int[] dp = new int[amount + 1];
Arrays.fill(dp, amount + 1); dp[0] = 0;
for (int c : coins)
    for (int a = c; a <= amount; a++)
        dp[a] = Math.min(dp[a], dp[a - c] + 1);
return dp[amount] > amount ? -1 : dp[amount];
```
```java
// 0/1 Knapsack (space-optimized): iterate weight DESC to reuse each item once
int[] dp = new int[W + 1];
for (int i = 0; i < n; i++)
    for (int w = W; w >= wt[i]; w--)
        dp[w] = Math.max(dp[w], val[i] + dp[w - wt[i]]);
```

## 0/1 vs Unbounded (a classic trap)
- **0/1** (each item once): iterate capacity **descending**.
- **Unbounded** (reuse items): iterate capacity **ascending**.

## Interview Questions
- **Coin change vs 0/1 knapsack loop order?** Unbounded iterates capacity ascending (reuse); 0/1 descending (use once).
- **How recognize a DP pattern?** Match the problem to a known family (knapsack, LCS, grid, interval) to get state + recurrence.
- **LCS state and recurrence?** `dp[i][j]`; if chars match `1 + dp[i-1][j-1]`, else `max(dp[i-1][j], dp[i][j-1])`.

## Related Topics
- [[DP Fundamentals]] · [[Memoization vs Tabulation]] · [[Greedy vs DP]]

## Quick Revision
- Patterns: 1D, 0/1 & unbounded knapsack, LCS/edit distance, grid, interval, bitmask, tree DP. Match problem -> pattern -> state/recurrence. 0/1 = capacity DESC, unbounded = ASC.
