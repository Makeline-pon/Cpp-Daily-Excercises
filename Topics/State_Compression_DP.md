# State Compression DP

## Introduction
State Compression DP (often referred to as Bitmask DP) is a technique used when the state can be represented as a binary string (usually of length $\le 20$). Each bit in an integer represents a boolean state (e.g., whether a node is visited, or the value of a variable).

## Key Ideas
*   **State Representation**: Use an integer `mask` to represent the current state. For example, `mask = 5` (binary `101`) means the 0-th and 2-nd bits are set.
*   **Transitions**: Shift the mask left/right or use bitwise AND/OR/XOR to transition between states.
*   **Valid State Filtering**: In problems requiring "no consecutive 1s", we can precompute all valid masks using `(mask & (mask << 1)) == 0`.

## Related Problems
*   [Day 1: Binary String Coloring and Energy Second Moment on Hypercube](../Day%201/problem_en.md)