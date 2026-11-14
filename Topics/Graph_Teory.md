# Graph Theory (Basic)

## Introduction
A graph $G = (V, E)$ consists of a set of vertices $V$ and a set of edges $E$. Graphs are used to model pairwise relations between objects. In competitive programming, many real-world problems can be abstracted into graph models.

## Key Concepts

1.  **Directed / Undirected**: 
    *   In an undirected graph, edges have no direction, meaning $(u, v)$ is the same as $(v, u)$.
    *   In a directed graph (digraph), edges have a specific direction, represented as ordered pairs $(u, v)$.
2.  **Weighted / Unweighted**: Edges may have associated weights (or costs), representing distance, time, or capacity.
3.  **Degree**: The number of edges connected to a vertex. In a directed graph, it's divided into in-degree and out-degree.
4.  **Connected Components**: A maximal set of vertices where there is a path between every pair of vertices. A graph can have one or multiple connected components.
5.  **Tree**: A connected acyclic undirected graph. Any two vertices in a tree are connected by exactly one simple path.

## Graph Representations
*   **Adjacency Matrix**: A 2D array `graph[u][v]` where `graph[u][v] = 1` (or a weight) if there is an edge between $u$ and $v$, and 0 otherwise. It takes $O(V^2)$ space, suitable for dense graphs.
*   **Adjacency List**: An array of lists, where `adj[u]` stores all neighbors of $u$. It takes $O(V + E)$ space, suitable for sparse graphs. This is the most commonly used representation in competitive programming.

## Related Problems
*   [Day 2: Bipartite Coloring and Component Counting](../Day%202/problem.md)
