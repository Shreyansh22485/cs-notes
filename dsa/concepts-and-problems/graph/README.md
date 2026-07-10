# Graph Concepts & Problems

This directory contains concepts and problems related to graph algorithms, traversals, shortest paths, and advanced topological structures.

## Sub-Concept Index

Below is a detailed guide to all graph sub-concepts implemented in this repository. Click on any topic to view its detailed concept notes and code implementations:

| Topic | Description | Key Algorithms / Concepts |
| :--- | :--- | :--- |
| [BFS & DFS](bfs-dfs) | Fundamental graph traversals | Level-order queues (BFS) and recursive backtracks (DFS) |
| [0-1 BFS](0-1-bfs) | Shortest paths for weights in `{0, 1}` | Deque implementation (push-front for 0, push-back for 1) |
| [Multi-Source BFS](multi-source-bfs) | Simultaneous traversal from multiple nodes | Distance maps and queue initialization from multiple start nodes |
| [Topological Sort](topological-sort) | Linear ordering of directed acyclic graphs | Kahn's Algorithm (indegrees) and DFS-based ordering |
| [Cycle Detection](cycle-detection) | Checking for circular paths | DFS back-edges, BFS node indegrees, Union-Find |
| [Bipartite Graph](bipartite-graph) | Two-coloring graphs | Odd-length cycle check using BFS / DFS coloring |
| [Dijkstra's Algorithm](dijkstra's%20algorithm) | Single-source shortest path | Priority Queue (Min-Heap) for non-negative weights |
| [Bellman-Ford](bellman-ford) | Shortest path with negative weight support | Edge relaxation $N-1$ times, negative cycle detection |
| [Floyd-Warshall](floyd-warshall) | All-pairs shortest paths | Dynamic Programming matrix relaxation: $O(V^3)$ |
| [Disjoint Set Union (DSU)](disjoint-set-union) | Equivalence classes and connectivity | Path compression and union-by-rank / size |
| [Minimum Spanning Tree](minimum-spanning-tree) | Spanning forest with minimum edge weight sum | Kruskal's (DSU) and Prim's (greedy priority queue) |
| [Diameter of Undirected Graph](diameter-of-an-undirected-graph) | Longest shortest path between any two vertices | Double-BFS approach for trees, general tree DP |
| [Eulerian Path & Circuit](euler-path) | Traversing every edge exactly once | Hierholzer's Algorithm, degree conditions |
| [Kosaraju's Algorithm](kosaraju-algorithm) | Finding Strongly Connected Components (SCCs) | Double-DFS on transposed graph |

---


