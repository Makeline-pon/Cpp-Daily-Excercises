# Day 1: Binary String Coloring and Energy Second Moment on Hypercube

## Problem Statement
Given a $d$-dimensional hypercube graph $Q_d = (V, E)$, where the total number of nodes is $N = 2^d$. Nodes are numbered from $0$ to $N-1$. For any two nodes $u, v$, there is an undirected edge $(u, v) \in E$ if and only if their binary representations differ in exactly one bit. The distance $\text{dist}_G(u, v)$ between two nodes is defined as the number of differing bits in their binary representations (i.e., the Hamming distance).

Each node $i \in V$ is assigned a length-$K$ binary string $\mathbf{s}_i = (s_{i,1}, s_{i,2}, \dots, s_{i,K})$, where $s_{i,k} \in \{0, 1\}$.

We need to assign values to all nodes satisfying the following three constraints:

1. **Local No-Consecutive-1 Constraint**:
   For any node $i$ and any $k \in [1, K-1]$, adjacent positions cannot be both $1$. Formally:

$$
s_{i,k} \cdot s_{i,k+1} = 0
$$

2. **Long-range Parity Constraints**:
   Given a distance threshold $D$ and $M$ parity rules.
   The input provides $M$ lines, each containing a constraint. For a given dimension set $S_{uv} = \{k_1, \dots, k_L\}$ and target constant $P_{uv}$, it must satisfy:

$$
\bigoplus_{k \in S_{uv}} (s_{u,k} \land s_{v,k}) = P_{uv}
$$

   where $\oplus$ denotes XOR and $\land$ denotes logical AND.
   *Note: This constraint only takes effect if $\text{dist}_G(u, v) \le D$. The input guarantees that all provided constraint pairs satisfy this distance condition.*

3. **Head-Tail Mirror Symmetry Constraint**:
   Let node $0$ (binary all 0s) and node $N-1$ (binary all 1s) be the head and tail nodes of the graph. Their binary strings must satisfy central symmetry:

$$
\forall k \in [1, K], \quad s_{0,k} = s_{N-1, K+1-k}
$$

Define the global energy functional $E(\mathbf{S})$ as:

$$
E(\mathbf{S}) = \sum_{i=0}^{N-1} \sum_{k=1}^K w_{i,k} \cdot s_{i,k} + \lambda \sum_{(u,v) \in E} J_{uv} \cdot \left( \sum_{k=1}^K s_{u,k} \cdot s_{v,k} \right)
$$

where:
- $w_{i,k}$ is the weight of node $i$ at dimension $k$.
- $J_{uv}$ is the interaction weight of edge $(u, v)$.
- $\lambda$ is the global coupling constant.

Calculate the sum of the second moments of the energy over all valid configurations $\mathbf{S}$, i.e.:

$$
\text{Answer} = \sum_{\mathbf{S} \in \mathcal{S}_{\text{valid}}} \left( E(\mathbf{S}) \right)^2 \pmod{998244353}
$$

If no valid configuration exists, output $0$.

## Input Format

The first line contains four integers $N, K, D, \lambda$.
Where $N = 2^d$ is guaranteed, $1 \le d \le 16$, $1 \le K \le 10$, $0 \le D \le d$, $0 \le \lambda \le 10^9$.

The second line contains $N \times K$ integers, providing $w_{i,k}$ in row-major order (node by node, then dimension by dimension).

The next $N \cdot d / 2$ lines, each containing three integers $u, v, J_{uv}$, represent an undirected edge in the hypercube and its interaction weight. The input guarantees that exactly all edges in the hypercube graph $Q_d$ are given.

The next line contains an integer $M$, representing the number of long-range parity constraints.
The following $M$ lines each describe a constraint. The format is:
$u, v, L, P, k_1, k_2, \dots, k_L$
where $u, v$ are node indices, $L$ is the number of dimensions involved, $P$ is the parity constant, and $k_1, \dots, k_L$ are the specific dimension indices.
If $L=1$, it is the simplified model (single-dimension constraint); if $L \ge 2$, it is the general model (set XOR constraint).

The last line contains $K$ integers used to confirm the mirror mapping relationship (usually all 0s, representing the standard reverse mapping $k \to K+1-k$).

## Output Format

Output a single integer, representing the answer modulo $998244353$.

## Samples

### Sample 1

**Input**
```text
2 2 1 1
1 2 3 4 5 6 7 8
0 1 1
0 2 1
1 3 1
2 3 1
0
0 0
```
**Output**
```text
0
```

### Sample 2

**Input**
```text
4 3 2 2
5 10 15 20 25 30 35 40 45 50 55 60
0 1 5
0 2 10
1 3 15
2 3 20
0
0 0 0
```
**Output**
```text
4280625
```

## Constraints and Hints

| Parameter | Constraints | Description |
| :--- | :--- | :--- |
| $d$ (Hypercube dimension) | $1 \le d \le 16$ | Graph is a $d$-dimensional hypercube, node count $N = 2^d$ (up to 65536). |
| $K$ (State dimension) | $1 \le K \le 10$ | Binary string length. Valid states count $\le F_{K+2}$ (no consecutive 1s). |
| $D$ (Distance threshold) | $0 \le D \le d$ | Only node pairs with Hamming distance $\le D$ have long-range constraints. |
| $\lambda$ (Global coupling) | $0 \le \lambda \le 10^9$ | Global scaling factor for edge interactions, modulo $998244353$. |
| $w_{i,k}$ (Node weight) | $1 \le w_{i,k} \le 10^4$ | Base energy when the $k$-th bit of node $i$ is 1. |
| $J_{uv}$ (Edge weight) | $1 \le J_{uv} \le 10^4$ | Interaction energy when both corresponding bits of $u, v$ are 1. |
| $P_{uv}$ (Parity target) | $\in \{0, 1\}$ | Target XOR result for long-range constraints. |
| Intermediate variables | $< 2^{63}$ | Use 64-bit integer (`long long`), modulo after each step to avoid overflow. |
| Final Answer | $\in [0, 998244353)$ | Sum of second moments of energy modulo $998244353$. |

**Algorithm Hints:**
Since $N \le 65536$, brute force over $2^{N \times K}$ global states is infeasible. The core is **State Compression DP utilizing the hypercube structure**:
1. Precompute all valid binary states for a single node (filtering out illegal strings with consecutive 1s).
2. Exploit the structural properties of the hypercube (it's a bipartite graph, and nodes can be layered by the number of 1s in their binary representation) for DP transitions.
3. During transitions, maintain `cnt` (number of ways), `sum1` (sum of energy), and `sum2` (sum of squared energy). Use the expansion of $(E+\Delta)^2$ to accumulate the second moment.
4. Finally, validate the head-tail mirror constraint and long-range parity constraints to filter out invalid schemes.

## Difficulty

1.00
