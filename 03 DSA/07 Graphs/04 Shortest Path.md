---
title: Shortest Path
aliases:
  - Shortest Path
  - Dijkstra
domain: DSA
module: Graphs
status: Learning
difficulty: Hard
priority: High
interview: 4
revision: Weekly
order: 4
tags:
  - dsa
related:
  - "[[BFS]]"
---

# Shortest Path

## Overview
Finding the minimum-cost path between vertices. The right algorithm depends on whether the graph is weighted and whether weights can be negative.

## Why It Matters
Shortest-path questions (maps, networks, "min cost to reach") are common and test whether you pick the correct algorithm for the graph's properties.

## Algorithm Selection
| Graph | Algorithm | Complexity |
|-------|-----------|-----------|
| Unweighted | [[BFS]] | O(V + E) |
| Weighted, non-negative | **Dijkstra** (min-heap) | O((V+E) log V) |
| Weighted, negative edges | **Bellman-Ford** | O(V·E) |
| All pairs | **Floyd-Warshall** | O(V³) |

## Dijkstra (min-heap)
```java
int[] dist = new int[V]; Arrays.fill(dist, INF); dist[src] = 0;
PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[1] - b[1]); // {node, dist}
pq.offer(new int[]{src, 0});
while (!pq.isEmpty()) {
    int[] cur = pq.poll(); int u = cur[0], d = cur[1];
    if (d > dist[u]) continue;                 // stale entry
    for (int[] e : adj.get(u)) {               // e = {v, weight}
        int v = e[0], w = e[1];
        if (dist[u] + w < dist[v]) { dist[v] = dist[u] + w; pq.offer(new int[]{v, dist[v]}); }
    }
}
```

## Key Points
- **Dijkstra fails with negative edges** — use Bellman-Ford, which also **detects negative cycles**.
- BFS = Dijkstra when all weights are equal.
- A* adds a heuristic to Dijkstra for goal-directed search.

## Interview Questions
- **Which algorithm for which graph?** BFS (unweighted), Dijkstra (non-negative weights), Bellman-Ford (negative), Floyd-Warshall (all pairs).
- **Why does Dijkstra fail on negative edges?** Its greedy "finalize the min" assumption breaks; a later negative edge could improve a finalized node.
- **How detect a negative cycle?** Bellman-Ford: a relaxation still improves after V-1 passes.

## Related Topics
- [[BFS]] · [[Heap]] · [[Graph Representation]]

## Quick Revision
- Unweighted -> BFS; non-negative -> Dijkstra (min-heap, O((V+E)logV)); negative -> Bellman-Ford (O(VE), detects neg cycle); all-pairs -> Floyd-Warshall O(V³). Dijkstra can't handle negatives.
