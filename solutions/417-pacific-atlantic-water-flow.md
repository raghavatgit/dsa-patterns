# 417. Pacific Atlantic Water Flow

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(m * n)

## TypeScript Implementation
```typescript
export function pacificAtlantic(heights: number[][]): number[][] {
    const m = heights.length;
    const n = heights[0].length;
    const pacific = Array.from({ length: m }, () => new Array(n).fill(false));
    const atlantic = Array.from({ length: m }, () => new Array(n).fill(false));

    const dfs = (r: number, c: number, visited: boolean[][]) => {
        visited[r][c] = true;
        const dirs = [[0, 1], [0, -1], [1, 0], [-1, 0]];
        for (const [dr, dc] of dirs) {
            const nr = r + dr;
            const nc = c + dc;
            if (nr >= 0 && nr < m && nc >= 0 && nc < n && !visited[nr][nc] && heights[nr][nc] >= heights[r][c]) {
                dfs(nr, nc, visited);
            }
        }
    };

    for (let r = 0; r < m; r++) {
        dfs(r, 0, pacific);
        dfs(r, n - 1, atlantic);
    }
    for (let c = 0; c < n; c++) {
        dfs(0, c, pacific);
        dfs(m - 1, c, atlantic);
    }

    const result: number[][] = [];
    for (let r = 0; r < m; r++) {
        for (let c = 0; c < n; c++) {
            if (pacific[r][c] && atlantic[r][c]) result.push([r, c]);
        }
    }

    return result;
}
```
