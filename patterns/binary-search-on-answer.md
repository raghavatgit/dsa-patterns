# Pattern: Binary Search on Answer

## Theoretical Basis
When a problem asks to find the minimum possible maximum, or maximum possible minimum:
If a predicate $P(X)$ satisfies monotonicity:
$$P(X) = \text{true} \implies P(X + 1) = \text{true}$$
we can binary search over the output range $[\text{low}, \text{high}]$ in $O(\log(\text{range}) \times T_{predicate})$.

## Canonical Problems
- Split Array Largest Sum (LeetCode 410)
- Capacity To Ship Packages Within D Days (LeetCode 1011)
- Koko Eating Bananas (LeetCode 875)
- Painter's Partition Problem
- Aggressive Cows (SPOJ)
