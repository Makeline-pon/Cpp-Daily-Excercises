\# Graph Structures: Hypercube



\## Introduction

A \\(d\\)-dimensional hypercube \\(Q\_d\\) has \\(N = 2^d\\) nodes. Two nodes are connected if their binary representations differ in exactly one bit.



\## Key Properties

1\.  \*\*Edges\*\*: \\(d \\cdot 2^{d-1}\\) undirected edges. Each node has degree \\(d\\).

2\.  \*\*Bipartite Nature\*\*: The graph is bipartite. Nodes can be partitioned by the parity of the number of 1s in their binary representation.

3\.  \*\*Layering\*\*: Nodes can be layered by the number of 1s (the bitcount). The \\(i\\)-th layer has \\(\\binom{d}{i}\\) nodes.



\## Related Problems

\*   \[Day 1: Binary String Coloring and Energy Second Moment on Hypercube](../Day%201/problem\_en.md)

