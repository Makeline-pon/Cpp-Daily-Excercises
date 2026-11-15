# Day 2: Lexicographically Smallest Bipartite Coloring

## Problem Statement

You are given an undirected graph $G = (V, E)$ with $N$ vertices and $M$ edges. The graph does not contain self-loops or multiple edges.

You need to assign a color $c_i \in \{0, 1\}$ to each vertex $i \in V$ satisfying the following conditions:
1. The graph must be **properly 2-colored** (i.e., for every edge $(u, v) \in E$, $c_u \neq c_v$). If the graph cannot be properly 2-colored, output `-1`.
2. The color assignment must be **lexicographically smallest**. Since the colors are binary, we consider the sequence of colors $(c_0, c_1, \dots, c_{N-1})$ as a binary number. You need to minimize this binary number. (For example, a sequence starting with $0$ is smaller than one starting with $1$).

## Input Format

The first line contains two integers $N$ and $M$.
The next $M$ lines each contain two integers $u$ and $v$, representing an undirected edge between vertex $u$ and vertex $v$.

## Output Format

Output $N$ space-separated integers $c_0, c_1, \dots, c_{N-1}$, representing the lexicographically smallest valid coloring. If no valid coloring exists, output `-1`.

## Samples

### Sample 1

**Input**
~~~text
4 3
1 2
2 3
3 0
~~~

**Output**
~~~text
0 0 1 0
~~~

**Explanation**
The graph is a path 1-2-3-0. The valid colorings are [0, 0, 1, 0] (starting with 0) and [1, 1, 0, 1] (starting with 1). The lexicographically smallest is [0, 0, 1, 0].

### Sample 2

**Input**
~~~text
3 3
0 1
1 2
2 0
~~~

**Output**
~~~text
-1
~~~

## Constraints and Hints

| Parameter | Constraints | Description |
| :--- | :--- | :--- |
| $N$ | $1 \le N \le 2 \times 10^5$ | Number of vertices. |
| $M$ | $0 \le M \le 2 \times 10^5$ | Number of edges. |

**Algorithm Hints:**
1. The graph may consist of multiple connected components.
2. To make the color array lexicographically smallest, we should prioritize minimizing the color of the vertex with the smallest index.
3. For a connected component, once the color of one vertex is fixed, the colors of all other vertices in the component are uniquely determined (up to swapping 0 and 1).
4. Therefore, for each connected component, let the vertex with the smallest index in that component be the root. We should try to assign color $0$ to this root. If it leads to a valid 2-coloring, we keep it; otherwise, we assign color $1$ to the root. (Notice that if the component is isolated, we just assign 0).
5. Use BFS/DFS to traverse and check.

## Difficulty

**Difficulty: 1.20** - Normal

## Tags

[![Graph Theory](https://img.shields.io/badge/Graph%20Theory-brightgreen?style=flat-square)](../Topics/Graph_Theory.md)
[![Bipartite Graph](https://img.shields.io/badge/Bipartite%20Graph-blue?style=flat-square)](../Topics/Bipartite_Graph.md)
[![Greedy Algorithm](https://img.shields.io/badge/Greedy-orange?style=flat-square)](../Topics/Greedy.md)
[![Breadth-First Search](https://img.shields.io/badge/BFS-purple?style=flat-square)](../Topics/BFS.md)
