# Combinatorics

## Introduction
Combinatorics is a fundamental area of mathematics and computer science that deals with counting, arrangement, and combination of elements. In competitive programming, it often involves finding the number of valid configurations, calculating probabilities, or applying combinatorial identities to optimize algorithms.

## Key Concepts in Competitive Programming

### 1. Permutations and Combinations
*   **Factorials and Binomial Coefficients**: \(n!\) and \(\binom{n}{k} = \frac{n!}{k!(n-k)!}\) are the building blocks. In modular arithmetic, they are computed using precomputed factorials and inverse factorials with Fermat's Little Theorem.
*   **Lucas Theorem**: Used to compute \(\binom{n}{k} \pmod p\) when \(n, k\) are very large and \(p\) is a small prime.

### 2. Fibonacci Sequence
The Fibonacci sequence \(F_n\) often arises in tiling problems, path counting, and counting binary strings with constraints. 
*   **No Consecutive 1s**: The number of valid binary strings of length \(K\) with no two consecutive 1s is exactly \(F_{K+2}\). This is a crucial optimization when precomputing states for **Bitmask DP**.

### 3. Inclusion-Exclusion Principle
Used to count the size of the union of multiple sets. It is widely applied in problems involving constraints like "at least one condition must be satisfied."

### 4. Parity and XOR
In problems involving bitwise operations, combinatorial counting can be used to determine the number of configurations yielding a specific XOR sum. 
*   **Linear Basis (XOR Basis)**: A technique to find the maximum XOR subset, count the number of distinct XOR sums, or determine if a target value can be formed by a set of numbers.
*   **Parity Constraints**: When applying constraints like \(\bigoplus (s_{u,k} \land s_{v,k}) = P\), we often use dynamic programming or graph connectivity (e.g., DSU with parity) to count valid assignments.

## Related Problems
*   [Day 1: Binary String Coloring and Energy Second Moment on Hypercube](../Day%201/problem.md)

## Further Reading and Templates
*   **Factorials & Inverses**: Precompute up to \(2 \times 10^6\) in \(O(N)\) time.
*   **Catalan Numbers**: \(C_n = \frac{1}{n+1}\binom{2n}{n}\), used in valid parenthesis sequences and binary tree counting.
