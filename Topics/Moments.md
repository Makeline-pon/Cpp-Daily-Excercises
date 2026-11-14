# Moments and Expectation

## Introduction
In combinatorial problems, we often need to calculate the sum of energies or the expected value. The "Second Moment" refers to the sum of squared values, $E(X^2)$.

## Key Techniques
When adding a new contribution $\Delta$ to the current state $E$, the square expands as:
$$
(E + \Delta)^2 = E^2 + 2E\Delta + \Delta^2
$$

To maintain the sum of squares of all possible configurations, we need to maintain:
1.  `cnt`: The number of ways to reach the current state.
2.  `sum1`: The sum of the first moment $\sum E$.
3.  `sum2`: The sum of the second moment $\sum E^2$.

The transition for adding a new node with energy $W$ and edge energy $V$ (total $\Delta = W + V$) is:
*   `new_sum2 = old_sum2 + 2 * old_sum1 * \Delta + old_cnt * \Delta^2`

## Related Problems
*   [Day 1: Binary String Coloring and Energy Second Moment on Hypercube](../Day%201/problem_en.md)