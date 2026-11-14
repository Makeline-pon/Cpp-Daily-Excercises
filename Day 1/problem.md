# Day 1: Binary Energy Moments

## Problem Statement

Let $G = (V, E)$ be an undirected graph with $N$ vertices and $M$ edges. Each vertex $i$ is assigned a $K$-bit binary string

$$
s_i = (s_{i,1}, s_{i,2}, \ldots, s_{i,K}) \in \{0, 1\}^K.
$$

A string is **legal** if it contains no two consecutive $1$s. Formally, for every $1 \le j < K$, it is not the case that $s_{i,j} = s_{i,j+1} = 1$.

For every vertex $i$ and bit $j$, a base energy $w_{i,j}$ is paid when $s_{i,j} = 1$. For every edge $(u,v) \in E$ with interaction weight $J_{u,v}$, an interaction energy

$$
J_{u,v} \sum_{j=1}^{K} s_{u,j} s_{v,j}
$$

is paid, and all interaction energies are multiplied by the global coupling factor $\lambda$. Thus the total energy of a configuration $S = (s_0, s_1, \ldots, s_{N-1})$ is

$$
E(S) = \sum_{i=0}^{N-1} \sum_{j=1}^{K} w_{i,j} s_{i,j}
+ \lambda \sum_{(u,v) \in E} J_{u,v} \sum_{j=1}^{K} s_{u,j} s_{v,j}.
$$

In addition, $Q$ long-range parity constraints are given. For a vertex $i$, define its state parity as

$$
p_i = s_{i,1} \oplus s_{i,2} \oplus \cdots \oplus s_{i,K},
$$

where $\oplus$ denotes bitwise XOR. Each constraint is a triple $(u, v, P)$ requiring

$$
p_u \oplus p_v = P.
$$

A configuration is **valid** if every vertex state is legal and all $Q$ parity constraints are satisfied. Compute the sum of squared energies over all valid configurations:

$$
\text{Answer} = \sum_{\text{valid } S} E(S)^2 \bmod 998244353.
$$

The value $D$ in the input is the maximum Hamming distance allowed between the binary labels of the endpoints of a listed parity constraint. It is a promise about the input; it does not change the required computation.

## Input Format

- The first line contains four integers $N$, $K$, $D$, and $\lambda$.
- The next $N$ lines each contain $K$ integers. The $i$-th of these lines lists $w_{i,1}, w_{i,2}, \ldots, w_{i,K}$.
- The next line contains the integer $M$.
- The next $M$ lines each contain three integers $u$, $v$, and $J_{u,v}$, describing an undirected edge. Vertices are numbered from $0$ to $N-1$.
- The next line contains the integer $Q$.
- The next $Q$ lines each contain three integers $u$, $v$, and $P$, describing one parity constraint.

The interaction graph is given explicitly by its edge list, so it may be a ring, a hypercube, or any other undirected graph.

## Output Format

Print a single integer: the sum of $E(S)^2$ over all valid configurations, modulo $998244353$.

## Samples

### Sample 1

**Input**

```text
3 2 2 1
1 2
2 1
1 1
3
0 1 1
1 2 1
2 0 1
3
0 1 0
1 2 1
0 2 1
```

**Output**

```text
54
```

### Sample 2

**Input**

```text
3 2 0 2
1 1
2 3
1 2
3
0 1 2
1 2 1
2 0 3
0
```

**Output**

```text
1506
```

## Constraints and Hints

The samples and the bundled local test cases use small ring-shaped graphs. The table below summarizes the parameter ranges of the full hypercube test family.

| Parameter | Constraints | Description |
| :--- | :--- | :--- |
| $d$ (Hypercube dimension) | $1 \le d \le 16$ | Graph is a $d$-dimensional hypercube, node count $N = 2^d$ (up to $65536$). |
| $K$ (State dimension) | $1 \le K \le 10$ | Binary string length. Valid states count $\le F_{K+2}$ (no consecutive $1$s). |
| $D$ (Distance threshold) | $0 \le D \le d$ | Only node pairs with Hamming distance $\le D$ have long-range constraints. |
| $\lambda$ (Global coupling) | $0 \le \lambda \le 10^9$ | Global scaling factor for edge interactions, modulo $998244353$. |
| $w_{i,k}$ (Node weight) | $1 \le w_{i,k} \le 10^4$ | Base energy when the $k$-th bit of node $i$ is $1$. |
| $J_{uv}$ (Edge weight) | $1 \le J_{uv} \le 10^4$ | Interaction energy when both corresponding bits of $u, v$ are $1$. |
| $P_{uv}$ (Parity target) | $\in \{0, 1\}$ | Target XOR result for long-range constraints. |
| Intermediate variables | $< 2^{63}$ | Use a $64$-bit integer (`long long`), and take the modulus after each step to avoid overflow. |
| Final Answer | $\in [0, 998244353)$ | Sum of second moments of energy modulo $998244353$. |

Additional guarantees:

- $0 \le M \le 6 \times 10^5$ and $0 \le Q \le 2 \times 10^5$.
- No edge is repeated, and no parity constraint is repeated.
- The mathematical definition of $E(S)$ uses ordinary integers. When implementing the sum, reduce modulo $998244353$ after each addition and multiplication.

### Algorithm Hints

Since $N \le 65536$, brute force over all $2^{N \times K}$ global states is infeasible. The core idea is **state-compression DP utilizing the hypercube structure**:

1. Precompute all valid binary states for a single node, filtering out illegal strings that contain consecutive $1$s.
2. Exploit the structural properties of the hypercube, which is bipartite and whose nodes can be layered by the number of $1$s in their binary labels, to organize the DP transitions.
3. During transitions, maintain `cnt` (the number of ways), `sum1` (the sum of energies), and `sum2` (the sum of squared energies). Use the expansion $(E+\Delta)^2 = E^2 + 2E\Delta + \Delta^2$ to accumulate the second moment.
4. Finally, enforce all long-range parity constraints and any additional boundary conditions required by the graph family, discarding invalid configurations.

## Difficulty

1.00
