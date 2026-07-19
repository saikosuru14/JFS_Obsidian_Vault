---
title: Union Find
aliases:
  - Union Find
  - Disjoint Set Union
  - DSU
domain: DSA
module: Graphs
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 6
tags:
  - dsa
related:
  - "[[Graphs Index|Graphs]]"
---

# Union Find (Disjoint Set Union)

## Overview
Union-Find maintains a collection of disjoint sets with two operations: **find** (which set is x in?) and **union** (merge two sets). With **path compression** + **union by rank/size**, both run in near-constant amortized time (inverse Ackermann, effectively O(1)).

## Why It Matters
It's the fast answer for dynamic connectivity: cycle detection in undirected graphs, connected components, and **Kruskal's MST**. Recognizing "group things / are these connected?" signals DSU.

## Implementation
```java
int[] parent, rank;
int find(int x) {
    if (parent[x] != x) parent[x] = find(parent[x]);   // path compression
    return parent[x];
}
boolean union(int a, int b) {
    int ra = find(a), rb = find(b);
    if (ra == rb) return false;                        // already connected -> cycle
    if (rank[ra] < rank[rb]) { int t = ra; ra = rb; rb = t; }
    parent[rb] = ra;                                   // union by rank
    if (rank[ra] == rank[rb]) rank[ra]++;
    return true;
}
```

## Optimizations
- **Path compression** — flatten the tree during `find`.
- **Union by rank/size** — attach the smaller tree under the larger.
- Together: amortized ~O(α(n)) ≈ O(1) per operation.

## Use Cases
- Connected components / number of provinces.
- **Cycle detection** in undirected graphs (union returns false).
- **Kruskal's MST** (add edge if endpoints are in different sets).
- Dynamic connectivity, account merging, grid percolation.

## Interview Questions
- **What does union-find do and how fast?** Tracks disjoint sets; find/union near O(1) amortized with compression + rank.
- **Detect a cycle in an undirected graph with DSU?** If both endpoints of an edge share a root, adding it forms a cycle.
- **Where is it used?** Kruskal's MST, connected components, dynamic connectivity.

## Related Topics
- [[Graph Representation]] · [[DFS]] · [[Topological Sort]]

## Quick Revision
- Disjoint sets with find/union; path compression + union by rank => ~O(1) amortized. Cycle detection (undirected), components, Kruskal's MST.
