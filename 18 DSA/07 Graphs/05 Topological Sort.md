---
title: Topological Sort
aliases:
  - Topological Sort
  - Topo Sort
domain: DSA
module: Graphs
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 5
tags:
  - dsa
related:
  - "[[DFS]]"
---

# Topological Sort

## Overview
A topological sort is a linear ordering of a **directed acyclic graph (DAG)** where every edge u -> v places u before v. It exists **only if the graph has no cycle**, so it doubles as a cycle detector.

## Why It Matters
It models dependency resolution: build order, task scheduling, course prerequisites, package installation. "Order things given dependencies" = topological sort.

## Kahn's Algorithm (BFS, in-degree)
```java
int[] indeg = new int[V];
for (int u = 0; u < V; u++) for (int v : adj.get(u)) indeg[v]++;
Queue<Integer> q = new ArrayDeque<>();
for (int u = 0; u < V; u++) if (indeg[u] == 0) q.offer(u);
List<Integer> order = new ArrayList<>();
while (!q.isEmpty()) {
    int u = q.poll(); order.add(u);
    for (int v : adj.get(u)) if (--indeg[v] == 0) q.offer(v);
}
if (order.size() != V) throw new IllegalStateException("cycle"); // not all placed
```

## DFS Approach
Do a DFS; push each node onto a stack in **post-order**; the reversed stack is a topological order.

## Cycle Detection
- **Kahn's**: if the output has fewer than V nodes, a cycle exists.
- **DFS**: a back edge (node in the current recursion stack) means a cycle.

## Interview Questions
- **When does a topological order exist?** Only for a DAG (no cycles).
- **Kahn's vs DFS?** BFS by in-degree (also detects cycles by count) vs DFS post-order reversed.
- **Real use case?** Course schedule / build order / task dependencies.

## Related Topics
- [[DFS]] · [[BFS]] · [[Graph Representation]]

## Quick Revision
- Linear order of a DAG with u before v for every edge. Kahn's (in-degree BFS; short output => cycle) or DFS post-order reversed. Dependency/build/course ordering.
