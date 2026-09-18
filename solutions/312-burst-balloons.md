# Problem: Burst Balloons (Interval DP)

## Problem Statement
You are given `n` balloons, indexed from `0` to `n - 1`. Each balloon is painted with a number on it represented by an array `nums`. You are asked to burst all the balloons. If you burst the `i`-th balloon, you will get `nums[i - 1] * nums[i] * nums[i + 1]` coins. Return the maximum coins you can collect by bursting the balloons wisely.

## Intuition & Approach
Reverse Interval Dynamic Programming:
1. Thinking forward (which balloon to burst *first*) couples left and right subproblems because bursting a balloon changes neighbours for adjacent balloons.
2. Think backwards: which balloon $k$ is burst *last* in the open interval $(i, j)$?
3. In that state, balloons $i$ and $j$ remain intact on either side of balloon $k$. The coins collected bursting $k$ last is `nums[i] * nums[k] * nums[j]`.
4. Recurrence:
   `dp[i][j] = max_{i < k < j} (dp[i][k] + dp[k][j] + nums[i] * nums[k] * nums[j])`
5. Pad array with 1 at both ends: `[1, ...nums, 1]`.
6. Time Complexity: $O(N^3)$ iterating over interval lengths, starts, and partition points. Space Complexity: $O(N^2)$ DP table.

## TypeScript Implementation

```typescript
export function maxCoins(nums: number[]): number {
  const padded = [1, ...nums, 1];
  const n = padded.length;
  const dp: number[][] = Array.from({ length: n }, () => new Array(n).fill(0));

  for (let len = 2; len < n; len++) {
    for (let i = 0; i < n - len; i++) {
      const j = i + len;
      for (let k = i + 1; k < j; k++) {
        const coins = dp[i][k] + dp[k][j] + padded[i] * padded[k] * padded[j];
        dp[i][j] = Math.max(dp[i][j], coins);
      }
    }
  }

  return dp[0][n - 1];
}
```
