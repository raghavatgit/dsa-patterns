# Pattern: Interval Dynamic Programming

## Structure
Interval DP solves subproblems on continuous ranges $[i, j]$ in increasing order of interval length:
`for len in 1..N: for i in 1..(N - len + 1): j = i + len - 1`

## Canonical Formulations
1. **Matrix Chain Multiplication**: Minimize multiplication cost by partitioning at $k \in [i, j-1]$.
2. **Burst Balloons**: Reverse thinking by choosing the *last* balloon $k \in [i, j]$ to burst.
3. **Minimum Cost to Merge Stones**: Knapsack on interval reduction steps.
