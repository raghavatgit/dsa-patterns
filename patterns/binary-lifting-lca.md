# Pattern: Binary Lifting and Lowest Common Ancestor (LCA)

## Overview
Binary Lifting is a dynamic programming technique on trees that precomputes $2^k$-th ancestors for every node.
It allows querying the $k$-th ancestor of any node or finding the Lowest Common Ancestor (LCA) of any two nodes in $O(\log N)$ time after $O(N \log N)$ preprocessing.

## Precomputation Invariant
Let `up[u][k]` denote the $2^k$-th ancestor of node $u$:
- Base case: `up[u][0] = parent[u]`
- Transition: `up[u][k] = up[up[u][k - 1]][k - 1]`
- Because $2^k = 2^{k-1} + 2^{k-1}$, jumping $2^k$ steps is equivalent to taking two consecutive jumps of $2^{k-1}$.

## Finding LCA in O(log N)
1. Ensure both nodes $u$ and $v$ are at the same depth: if $\text{depth}(u) < \text{depth}(v)$, lift $v$ by the depth difference using binary powers.
2. If $u == v$, return $u$.
3. Iterate $k$ backwards from $\log_2 N$ down to 0:
   - If `up[u][k] != up[v][k]`, lift both nodes simultaneously: `u = up[u][k]`, `v = up[v][k]`.
4. Return `up[u][0]` (their common immediate parent).
