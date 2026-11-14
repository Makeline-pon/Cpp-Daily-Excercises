# Bipartite Graph

## Introduction
A bipartite graph is a graph whose vertices can be divided into two disjoint and independent sets $U$ and $V$ such that every edge connects a vertex in $U$ to one in $V$.

## Key Properties
1.  **Odd Cycle Condition**: A graph is bipartite if and only if it does not contain any odd-length cycles.
2.  **2-Colorability**: A graph is bipartite if and only if it is 2-colorable (the vertices can be colored with two colors such that no two adjacent vertices share the same color).
3.  **No Edges Within Sets**: There are no edges connecting vertices within the same set.

## Algorithms
*   **BFS/DFS Coloring**: The standard algorithm to check if a graph is bipartite. We start at an arbitrary node, color it 0, and color all its neighbors 1. If we encounter a neighbor that already has the same color as the current node, the graph is not bipartite. This runs in $O(N + M)$ time.

## Related Problems
*   [Day 2: Bipartite Coloring and Component Counting](../Day%202/problem_en.md)
