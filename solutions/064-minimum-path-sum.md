# Problem: Minimum Path Sum

## Problem Statement
Given an `m x n` grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path. You can only move either down or right at any point in time.

## Intuition & Approach
1D Rolling Array Dynamic Programming:
1. Let `dp[c]` store the minimum path sum to cell in column `c` of the active row.
2. Initialization: `dp[c] = dp[c - 1] + grid[0][c]` for top row.
3. For subsequent rows:
   - `dp[0] += grid[r][0]` (moving down from above).
   - For $c > 0$: `dp[c] = min(dp[c] (down), dp[c - 1] (right)) + grid[r][c]`.
4. Time Complexity: $O(M \times N)$. Space Complexity: $O(N)$ 1D array.

## TypeScript Implementation

```typescript
export function minPathSum(grid: number[][]): number {
  const m = grid.length;
  const n = grid[0].length;
  const dp: number[] = new Array(n).fill(0);

  dp[0] = grid[0][0];
  for (let c = 1; c < n; c++) {
    dp[c] = dp[c - 1] + grid[0][c];
  }

  for (let r = 1; r < m; r++) {
    dp[0] += grid[r][0];
    for (let c = 1; c < n; c++) {
      dp[c] = Math.min(dp[c], dp[c - 1]) + grid[r][c];
    }
  }

  return dp[n - 1];
}
```
