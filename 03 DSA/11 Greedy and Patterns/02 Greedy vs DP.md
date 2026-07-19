---
title: Greedy vs DP
aliases:
  - Greedy vs DP
domain: DSA
module: Greedy and Patterns
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Greedy Approach]]"
---

# Greedy vs DP

## Overview
Both greedy and dynamic programming solve optimization problems with optimal substructure, but they differ in how they choose: **greedy commits** to one locally optimal choice and never looks back; **DP explores** all choices and keeps the best.

## Why It Matters
The most common mistake is applying greedy where DP is required (e.g., coin change with arbitrary denominations). Knowing how to distinguish them — and prove greedy correct — is a frequent interview theme.

## Comparison
| | Greedy | Dynamic Programming |
|--|--------|---------------------|
| Choice | one local optimum, no revisit | tries all options, caches best |
| Requires | greedy-choice property | overlapping subproblems |
| Speed | usually faster (O(n log n)) | more work (poly, but larger) |
| Risk | may be wrong | correct if recurrence is right |
| Correctness | needs a proof (exchange arg) | follows from the recurrence |

## The Classic Contrast: Coin Change
- **Canonical coins** (1, 5, 10, 25): greedy (largest-first) works.
- **Arbitrary coins** (e.g., 1, 3, 4 for amount 6): greedy gives 4+1+1=3 coins, but DP finds 3+3=2. **Greedy fails -> use DP.**

## How To Decide
1. Try greedy; look for a counterexample.
2. If a local choice can be regretted later, you likely need DP.
3. If you can prove the greedy choice is always safe (exchange argument), greedy is fine and simpler.

## Interview Questions
- **Greedy vs DP core difference?** Greedy commits to a local optimum; DP explores all options and memoizes.
- **Example where greedy fails but DP works?** Coin change with non-canonical denominations.
- **How to justify greedy?** Prove the greedy-choice property (exchange argument) — don't just assume it.

## Related Topics
- [[Greedy Approach]] · [[Common DP Patterns]] · [[DP Fundamentals]]

## Quick Revision
- Greedy: commit locally, fast, needs proof. DP: explore all + cache, always correct with the right recurrence. Coin change (arbitrary coins) = greedy fails, DP wins. If a choice can be regretted, use DP.
