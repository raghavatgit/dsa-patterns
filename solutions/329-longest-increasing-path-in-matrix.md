# Problem: Longest Increasing Path in a Matrix

## Problem Statement
Given an `m x n` integers matrix, return the length of the longest increasing path in matrix. From each cell, you can either move in four directions: left, right, up, or down. You may not move diagonally or move outside the boundary.

## Intuition & Approach
Memoized Depth First Search on DAG:
1. Because path movements must be strictly increasing, the graph contains no cycles (it forms a Directed Acyclic Graph).
2. For each cell `(r, c)`, let `memo[r][c]` be the length of the longest increasing path starting at `(r, c)`.
3. If `memo[r][c]` is already calculated, return it immediately in $O(1)$ time.
4. Explore 4 orthogonal neighbours `(nr, nc)`. If `matrix[nr][nc] > matrix[r][c]`, recurse: `path = 1 + dfs(nr, nc)`.
5. Maximize across all 4 directions and store in `memo[r][c]`.
6. Time Complexity: $O(M \times N)$ visiting each state once. Space Complexity: $O(M \times N)$ memoization table and recursion stack.

## TypeScript Implementation

```typescript
export function longestIncreasingPath(matrix: number[][]): number {
  const m = matrix.length;
  if (m === 0) return 0;
  const n = matrix[0].length;
  if (n === 0) return 0;

  const memo: number[][] = Array.from({ length: m }, () => new Array(n).fill(0));
  const dirs = [[0, 1], [0, -1], [1, 0], [-1, 0]];

  function dfs(r: number, c: number): number {
    if (memo[r][c] !== 0) return memo[r][c];

    let maxLen = 1;
    for (const [dr, dc] of dirs) {
      const nr = r + dr;
      const nc = c + dc;
      if (nr >= 0 && nr < m && nc >= 0 && nc < n && matrix[nr][nc] > matrix[r][c]) {
        maxLen = Math.max(maxLen, 1 + dfs(nr, nc));
      }
    }

    memo[r][c] = maxLen;
    return maxLen;
  }

  let longest = 0;
  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      longest = Math.max(longest, dfs(r, c));
    }
  }

  return longest;
}
```
