---
title: DFS
aliases:
  - DFS
  - Depth-First Search
domain: DSA
module: Graphs
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[Graph Representation]]"
  - "[[Topological Sort]]"
---

# DFS (Depth-First Search)

## Overview
DFS explores as far as possible along each branch before backtracking, using recursion (the call stack) or an explicit [[Stack|stack]] plus a visited set. It naturally exposes structure: cycles, components, and ordering.

## Why It Matters
DFS underlies cycle detection, topological sort, connected components, and most backtracking/grid problems. It's the second core graph traversal alongside BFS.

## Template
```java
boolean[] visited = new boolean[V];

void dfs(int u) {
    visited[u] = true;
    visit(u);
    for (int v : adj.get(u))
        if (!visited[v]) dfs(v);
}
```
Iterative version uses an explicit stack; on grids, recurse in 4 directions.

## Complexity
O(V + E) time; O(V) space (visited + recursion stack up to O(V) deep).

## Use Cases
- Connected components / number of islands.
- **Cycle detection** — recursion-stack (directed) or parent-tracking (undirected).
- **[[Topological Sort]]** — post-order of a DAG, reversed.
- Path existence, flood fill, [[Backtracking]].

## Cycle Detection (directed)
Track three states (unvisited/in-progress/done); encountering an in-progress node = back edge = cycle.

## BFS vs DFS
- **DFS** — deep, memory O(depth), great for connectivity/cycles/topo/backtracking.
- **[[BFS]]** — wide, finds shortest unweighted path.

## Interview Questions
- **Recursive vs iterative DFS?** Same result; recursion uses the call stack (risk of overflow on deep graphs), iterative uses an explicit stack.
- **Detect a cycle in a directed graph?** DFS with in-progress marking (back edge -> cycle), or Kahn's algorithm.
- **DFS vs BFS?** DFS for connectivity/cycles/topo/backtracking; BFS for shortest unweighted path/levels.

## Related Topics
- [[Topological Sort]] · [[BFS]] · [[Backtracking]] · [[Stack]]

## Quick Revision
- Go deep + backtrack via recursion/stack + visited. O(V+E). Components, cycle detection, topo sort, flood fill, backtracking. Deep graphs risk stack overflow.
