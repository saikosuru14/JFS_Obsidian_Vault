---
title: Graph Representation
aliases:
  - Graph Representation
domain: DSA
module: Graphs
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Graphs Index|Graphs]]"
  - "[[BFS]]"
  - "[[DFS]]"
---

# Graph Representation

## Overview
How you store a graph determines the complexity of every operation. The two standard forms are the **adjacency list** (each vertex maps to its neighbors) and the **adjacency matrix** (a V×V grid of edge presence/weight).

## Why It Matters
Picking the right representation is the first decision in any graph problem. Most interview graphs are sparse, so the adjacency list is the default.

## Adjacency List vs Matrix
| | Adjacency List | Adjacency Matrix |
|--|----------------|------------------|
| Space | O(V + E) | O(V²) |
| Edge exists? | O(degree) | O(1) |
| Iterate neighbors | O(degree) | O(V) |
| Best for | sparse graphs (usual) | dense graphs / fast edge checks |

```java
// Adjacency list (most common)
List<List<Integer>> adj = new ArrayList<>();
for (int i = 0; i < V; i++) adj.add(new ArrayList<>());
adj.get(u).add(v);           // directed edge u -> v
adj.get(v).add(u);           // add reverse for undirected
```

## Graph Types
- **Directed vs undirected**; **weighted vs unweighted**; **cyclic vs acyclic** (DAG); **connected vs disconnected**.
- Special: **grid** graphs (matrix cells as nodes) — very common in interviews.

## Interview Questions
- **Adjacency list vs matrix?** List O(V+E) space, great for sparse; matrix O(V²) space with O(1) edge lookup, good for dense.
- **Which is more common in interviews?** Adjacency list (most graphs are sparse).
- **How model a grid as a graph?** Each cell is a node; edges to 4/8 adjacent cells.

## Related Topics
- [[BFS]] · [[DFS]] · [[Union Find]]

## Quick Revision
- Adjacency list O(V+E) (sparse, default) vs matrix O(V²) (dense, O(1) edge check). Note directed/weighted/cyclic. Grids = implicit graphs.
