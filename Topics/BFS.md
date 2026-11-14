# Breadth-First Search (BFS)

## Introduction
Breadth-First Search (BFS) is a fundamental graph traversal algorithm. It starts at an arbitrary node and explores all its neighbors first, then explores the neighbors of those neighbors, and so on.

## Key Ideas
*   **Queue**: BFS is typically implemented using a Queue (First-In, First-Out).
*   **Shortest Path**: In an unweighted graph, the first time BFS reaches a node, it is guaranteed to be via the shortest path from the starting node.
*   **Level Order**: BFS explores nodes in "levels" based on their distance from the starting node.

## Applications
*   Finding the shortest path in an unweighted graph.
*   Checking if a graph is bipartite (2-coloring).
*   Finding all connected components in a graph.
*   Topological sorting (Kahn's algorithm).

## Related Problems
*   [Day 2: Bipartite Coloring and Component Counting](../Day%202/problem.md)
