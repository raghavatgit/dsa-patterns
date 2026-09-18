# Pattern: Bitmask Dynamic Programming

## Overview
Bitmask DP is used when problem states involve tracking subsets of small size ($N \le 20$). An integer bitmask represents set membership: the $i$-th bit is 1 if item $i$ is included, and 0 if omitted.

## Canonical Operations
- Test membership of element $i$: `(mask & (1 << i)) != 0`
- Add element $i$: `mask | (1 << i)`
- Remove element $i$: `mask & ~(1 << i)`
- Toggle element $i$: `mask ^ (1 << i)`
- Iterate all subsets of a mask:
  ```cpp
  for (int sub = mask; sub > 0; sub = (sub - 1) & mask) {
      // Process submask
  }
  ```

## Canonical Problem: Traveling Salesperson Problem (TSP)
Given $N$ cities and distance matrix `dist[i][j]`, find minimum cost to visit all cities and return to origin:
- State: `dp[mask][u]` = minimum cost visiting subset `mask` ending at vertex `u`.
- Recurrence: `dp[mask | (1 << v)][v] = min(dp[mask | (1 << v)][v], dp[mask][u] + dist[u][v])`
- Complexity: $O(N^2 \cdot 2^N)$ vs brute force $O(N!)$.
