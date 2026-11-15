# Day 2: Dynamic Parity Network

## Problem Statement

You are given an initially empty undirected graph with \(N\) vertices, numbered from 0 to \(N-1\). You will receive \(M\) edge additions sequentially. Each edge addition is given as a pair of vertices $(u, v)$, indicating an undirected edge between \(u\) and \(v\).

After each edge addition, you need to answer:
1. Is the current graph bipartite? If it is **not** bipartite, output `-1` and terminate the program immediately.
2. If it is bipartite, output the number of **connected components** in the current graph.

## Input Format

The first line contains two integers \(N\) and \(M\), representing the number of vertices and the number of edge additions.
The next \(M\) lines each contain two integers \(u\) and \(v\), representing an undirected edge added between \(u\) and \(v\).

## Output Format

Output \(M\) lines. The \(i\)-th line is the answer after the \(i\)-th edge addition.
If the graph becomes non-bipartite at any step, output `-1` and the program should stop further processing.

## Samples

### Sample 1

**Input**
~~~text
4 4
0 1
1 2
0 2
2 3
~~~

**Output**
~~~text
3
2
-1
~~~

**Explanation**
- After adding 0-1: 1 edge, bipartite. Components = 3.
- After adding 1-2: 2 edges, path 0-1-2, bipartite. Components = 2.
- After adding 0-2: triangle 0-1-2 formed, which is an odd cycle, not bipartite. Output -1 and stop.

## Constraints and Hints

| Parameter | Constraints | Description |
| :--- | :--- | :--- |
| \(N\) (Number of vertices) | \(1 \le N \le 2 \times 10^5\) | Number of vertices. |
| \(M\) (Number of edges) | \(1 \le M \le 2 \times 10^5\) | Number of additions. |
| \(u, v\) | \(0 \le u, v < N\) | Edge endpoints. |

**Algorithm Hints:**
1. Do **not** run BFS/DFS after each addition; the time complexity would be \(O(M(N+M))\), which will cause Time Limit Exceeded (TLE).
2. Use a **Disjoint Set Union (DSU) with Parity** to maintain the relative color of each vertex compared to its component's root.
3. Maintain an array `dist[x]` representing the parity of the path from \(x\) to its root. Use path compression to update `dist[x]`.
4. When adding an edge $(u, v)$:
    - Find their roots. If they are in the same component, check if the parity is consistent.
    - If they are in different components, merge them and update the parity accordingly. The number of components decreases by 1.

## Difficulty

**Difficulty: 1.30** - Hard (Normal+)

## Tags

[![Graph Theory](https://img.shields.io/badge/Graph%20Theory-brightgreen?style=flat-square)](../Topics/Graph_Theory.md)
[![Bipartite Graph](https://img.shields.io/badge/Bipartite%20Graph-blue?style=flat-square)](../Topics/Bipartite_Graph.md)
[![Disjoint Set Union](https://img.shields.io/badge/Disjoint%20Set%20Union-red?style=flat-square)](../Topics/DSU.md)
