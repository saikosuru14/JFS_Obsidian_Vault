---
title: Backtracking
aliases:
  - Backtracking
domain: DSA
module: Recursion and Backtracking
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Recursion]]"
---

# Backtracking

## Overview
Backtracking builds candidates incrementally and abandons ("backtracks") a partial candidate as soon as it can't lead to a valid solution. It's a systematic DFS over a decision tree with the pattern **choose -> explore -> un-choose**.

## Why It Matters
It's the template for permutations, combinations, subsets, N-Queens, sudoku, word search, and constraint problems — a large interview category.

## Template
```java
void backtrack(State state, List<Result> out) {
    if (isComplete(state)) { out.add(snapshot(state)); return; }
    for (Choice c : choices(state)) {
        if (!isValid(c, state)) continue;   // prune
        apply(c, state);                    // choose
        backtrack(state, out);              // explore
        undo(c, state);                     // un-choose (backtrack)
    }
}
```

## Example: Subsets
```java
void subsets(int[] nums, int start, List<Integer> cur, List<List<Integer>> res) {
    res.add(new ArrayList<>(cur));          // record every node
    for (int i = start; i < nums.length; i++) {
        cur.add(nums[i]);                   // choose
        subsets(nums, i + 1, cur, res);     // explore
        cur.remove(cur.size() - 1);         // un-choose
    }
}
```

## Pruning
The key to efficiency: cut branches early with constraints (validity checks, bounds). N-Queens prunes columns/diagonals; sudoku prunes invalid digits.

## Complexity
Often exponential (O(2ⁿ) subsets, O(n!) permutations) — inherent to enumerating all solutions; pruning reduces the constant/branches.

## Interview Questions
- **What is backtracking?** DFS over a decision tree with choose/explore/un-choose, abandoning invalid partial solutions.
- **Backtracking vs DFS?** Backtracking is DFS that undoes choices to explore alternatives and enumerate solutions.
- **How to make it efficient?** Prune invalid branches as early as possible.
- **Typical complexity?** Exponential/factorial (subsets 2ⁿ, permutations n!).

## Related Topics
- [[Recursion]] · [[DFS]] · [[Divide and Conquer]]

## Quick Revision
- Incremental build + undo: choose/explore/un-choose over a decision tree. Prune early. Subsets/permutations/combinations, N-Queens, sudoku. Exponential by nature.
