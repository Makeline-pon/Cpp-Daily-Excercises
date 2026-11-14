# Day 2: Bipartite Coloring and Component Counting

## Problem Statement

You are given an undirected graph $G = (V, E)$ with $N$ vertices and $M$ edges. The graph does not contain self-loops or multiple edges. It is not guaranteed to be connected.

A graph is **bipartite** if its vertices can be partitioned into two disjoint sets $U$ and $V$ such that every edge connects a vertex in $U$ to one in $V$. 

Your task is to determine if the given graph is bipartite. If it is, calculate the number of valid bipartite colorings for the entire graph. Since the graph may consist of multiple connected components, the colorings of each component are independent of each other. 

Return the total number of valid colorings modulo $998244353$. If the graph is not bipartite, output `0`.

*(Note: For each connected component, there are exactly 2 valid ways to assign colors (e.g., swapping all black and white colors).)*

## Input Format

The first line contains two integers $N$ and $M$, where $N$ is the number of vertices and $M$ is the number of edges.
The next $M$ lines each contain two integers $u$ and $v$, representing an undirected edge between vertex $u$ and vertex $v$.

## Output Format

Output a single integer, representing the number of valid bipartite colorings modulo $998244353$. If the graph is not bipartite, output `0`.

## Samples

### Sample 1

**Input**
~~~text
4 3
0 1
1 2
2 3
~~~

**Output**
~~~text
2
~~~

**Explanation**
The graph is a single connected component (a path). There are 2 valid colorings: [0, 1, 0, 1] and [1, 0, 1, 0].

### Sample 2

**Input**
~~~text
4 4
0 1
1 2
2 3
3 0
~~~

**Output**
~~~text
2
~~~

**Explanation**
The graph is a cycle of length 4 (which is bipartite). There are 2 valid colorings.

### Sample 3

**Input**
~~~text
3 3
0 1
1 2
2 0
~~~

**Output**
~~~text
0
~~~

**Explanation**
The graph contains a triangle (an odd cycle), so it is not bipartite. Output 0.

## Constraints and Hints

| Parameter | Constraints | Description |
| :--- | :--- | :--- |
| $N$ (Number of vertices) | $1 \le N \le 2 \times 10^5$ | The number of vertices in the graph. |
| $M$ (Number of edges) | $0 \le M \le \min(2 \times 10^5, \frac{N(N-1)}{2})$ | The number of undirected edges. |
| $u, v$ | $0 \le u, v < N$ | Vertices are 0-indexed. |
| Final Answer | $\pmod{998244353}$ | The number of colorings modulo 998244353. |

**Algorithm Hints:**
1. A graph is bipartite if and only if it contains no odd-length cycles.
2. You can use Breadth-First Search (BFS) or Depth-First Search (DFS) to try to 2-color the graph.
3. If a conflict occurs during coloring (an edge connects two vertices of the same color), the graph is not bipartite.
4. If the graph is bipartite, and there are $C$ connected components, the answer is $2^C \pmod{998244353}$. Use binary exponentiation for fast calculation.

## Difficulty

**Difficulty: 1.20** - Normal

## Tags

[![Graph Theory](https://img.shields.io/badge/Graph%20Theory-brightgreen?style=flat-square)](../Topics/Graph_Theory.md)
[![Bipartite Graph](https://img.shields.io/badge/Bipartite%20Graph-blue?style=flat-square)](../Topics/Bipartite_Graph.md)
[![Breadth-First Search](https://img.shields.io/badge/BFS-purple?style=flat-square)](../Topics/BFS.md)