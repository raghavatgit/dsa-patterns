# 64. Minimum Path Sum

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(1) in-place

## TypeScript Implementation
```typescript
export function minPathSum(grid: number[][]): number {
    const m = grid.length;
    const n = grid[0].length;

    for (let i = 1; i < m; i++) grid[i][0] += grid[i - 1][0];
    for (let j = 1; j < n; j++) grid[0][j] += grid[0][j - 1];

    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            grid[i][j] += Math.min(grid[i - 1][j], grid[i][j - 1]);
        }
    }

    return grid[m - 1][n - 1];
}
```
