---
title: Graphs Index
aliases:
  - Graphs Index
  - Graphs
domain: DSA
module: Graphs
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - dsa
  - index
related:
  - "[[DSA Index|DSA]]"
  - "[[Graph Representation]]"
  - "[[Union Find]]"
---

# Graphs

> Module index - part of the [[DSA Index|DSA]] learning path.

## Overview
A graph is a set of vertices connected by edges — the most general data structure, modeling networks, dependencies, maps, and relationships. Master the representation, the two traversals (BFS/DFS), and a handful of algorithms (shortest path, topological sort, union-find) and most graph problems fall into place.

## Branches (expand each)
- **[[Graph Representation]]** — adjacency list vs matrix.
  - [[BFS]] — layer-by-layer traversal.
    - [[Shortest Path]] — unweighted (BFS), weighted (Dijkstra/Bellman-Ford).
  - [[DFS]] — depth-first traversal.
    - [[Topological Sort]] — ordering a DAG.
- **[[Union Find]]** — disjoint sets / connectivity.

## Learning Roadmap
1. [[Graph Representation]]
2. [[BFS]] -> [[Shortest Path]]
3. [[DFS]] -> [[Topological Sort]]
4. [[Union Find]]

## Prerequisites
- [[Trees Index|Trees]] · [[Stacks and Queues Index|Stacks and Queues]]

## Related
- [[DSA Index|DSA]]
- Next: [[Sorting and Searching Index|Sorting and Searching]]

## Quick Revision
- Vertices + edges (directed/weighted variants). Represent with adjacency list. Traverse via BFS (queue, shortest unweighted) / DFS (stack/recursion, cycles/topo). Algos: Dijkstra, topo sort, union-find.
