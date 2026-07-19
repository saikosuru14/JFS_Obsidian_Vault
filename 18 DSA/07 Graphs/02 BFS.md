---
title: BFS
aliases:
  - BFS
  - Breadth-First Search
domain: DSA
module: Graphs
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Graph Representation]]"
  - "[[Shortest Path]]"
---

# BFS (Breadth-First Search)

## Overview
BFS explores a graph level by level from a source, using a [[Queue|queue]] and a visited set. It visits all nodes at distance 1, then 2, and so on — which makes it find the **shortest path in an unweighted graph**.

## Why It Matters
BFS is the tool for shortest-path-by-edges, level-order problems, and "minimum steps" puzzles. On grids it's the default flood/shortest-move algorithm.

## Template
```java
Queue<Integer> q = new ArrayDeque<>();
boolean[] visited = new boolean[V];
q.offer(src); visited[src] = true;
int level = 0;
while (!q.isEmpty()) {
    int size = q.size();
    for (int i = 0; i < size; i++) {     // process one level
        int u = q.poll();
        for (int v : adj.get(u))
            if (!visited[v]) { visited[v] = true; q.offer(v); }
    }
    level++;
}
```
Mark visited **when enqueuing** (not dequeuing) to avoid adding a node twice.

## Complexity
O(V + E) time, O(V) space (queue + visited).

## Use Cases
- Shortest path in an **unweighted** graph (fewest edges).
- Level-order / minimum-steps problems (word ladder, rotting oranges).
- Connected components, bipartite check.
- Multi-source BFS (seed the queue with several starts).

## BFS vs DFS
- **BFS** — shortest unweighted path, level structure; queue; O(V) memory (can be wide).
- **[[DFS]]** — path existence, cycles, topological order; stack/recursion; O(h) memory.

## Interview Questions
- **Why does BFS find the shortest unweighted path?** It expands in order of edge-distance, so a node is first reached via a minimum-edge path.
- **When mark visited?** On enqueue, to prevent duplicate queue entries.
- **BFS vs DFS choice?** BFS for shortest/level; DFS for connectivity/cycles/topo.

## Related Topics
- [[Shortest Path]] · [[DFS]] · [[Queue]] · [[Graph Representation]]

## Quick Revision
- Level-by-level via queue + visited (mark on enqueue). O(V+E). Shortest path in unweighted graphs; level/min-steps; multi-source by seeding the queue.
