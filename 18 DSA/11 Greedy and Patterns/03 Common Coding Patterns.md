---
title: Common Coding Patterns
aliases:
  - Common Coding Patterns
domain: DSA
module: Greedy and Patterns
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Daily
order: 3
tags:
  - dsa
related:
  - "[[Greedy and Patterns Index|Greedy and Patterns]]"
---

# Common Coding Patterns

## Overview
Most interview problems are instances of a small set of reusable patterns. Learning to **recognize the pattern** from problem cues is far more effective than memorizing individual solutions.

## Why It Matters
Pattern recognition lets you map an unseen problem to a known technique in seconds — the core skill that separates prepared candidates.

## Pattern Catalog (with cues)
| Pattern | Cue | See |
|---------|-----|-----|
| **[[Two Pointers]]** | sorted array, pair/partition | Arrays |
| **[[Sliding Window]]** | contiguous subarray/substring + constraint | Arrays |
| **[[Fast and Slow Pointers]]** | cycle / middle of a list | Linked Lists |
| **[[Prefix Sum]]** | many range-sum queries | Arrays |
| **[[Hashing Patterns]]** | seen-before / counts / complement | Hashing |
| **[[Monotonic Stack]]** | next greater/smaller element | Stacks |
| **[[BFS]] / [[DFS]]** | trees, graphs, grids, levels | Graphs |
| **[[Heap]] (top-k)** | k largest/smallest, merge k | Trees |
| **[[Binary Search]]** | sorted, or monotonic answer space | Searching |
| **[[Backtracking]]** | all permutations/combinations/subsets | Recursion |
| **[[Common DP Patterns\|DP]]** | count/min/max over overlapping choices | DP |
| **[[Greedy Approach]]** | local optimum provably global | Greedy |
| **[[Union Find]]** | connectivity / grouping | Graphs |
| **[[Topological Sort]]** | ordering with dependencies | Graphs |

## How To Map A Problem
- "Contiguous subarray with sum/length constraint" -> sliding window.
- "Kth largest / top-k" -> heap.
- "Shortest path unweighted" -> BFS; "weighted non-negative" -> Dijkstra.
- "All combinations/permutations" -> backtracking.
- "Count ways / min cost with choices" -> DP.
- "Next greater element" -> monotonic stack.
- "Are these connected / number of groups" -> union-find/DFS.

## Interview Questions
- **How do you approach an unseen problem?** Identify cues -> match to a pattern -> adapt the template.
- **Cue for sliding window vs two pointers?** Contiguous window with a constraint vs sorted-pair/partition scan.
- **Top-k data structure?** A size-k heap.

## Related Topics
- [[Interview Strategy]] · [[Two Pointers]] · [[Sliding Window]] · [[Heap]]

## Quick Revision
- Learn cues -> pattern: two pointers, sliding window, fast/slow, prefix sum, hashing, monotonic stack, BFS/DFS, heap/top-k, binary search, backtracking, DP, greedy, union-find, topo sort.
