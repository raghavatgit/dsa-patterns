# 695. Max Area of Island

## Problem Statement
You are given an `m x n` binary matrix `grid`. An island is a group of `1`'s (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The **area** of an island is the number of cells with a value `1` in the island.

Return the maximum **area** of an island in `grid`. If there is no island, return `0`.

---

## TypeScript Implementation

```typescript
export function maxAreaOfIsland(grid: number[][]): number {
  const m = grid.length;
  const n = grid[0].length;
  let maxArea = 0;

  function dfs(r: number, c: number): number {
    if (r < 0 || r >= m || c < 0 || c >= n || grid[r][c] !== 1) {
      return 0;
    }
    grid[r][c] = 0; // sink the island in-place

    return (
      1 +
      dfs(r + 1, c) +
      dfs(r - 1, c) +
      dfs(r, c + 1) +
      dfs(r, c - 1)
    );
  }

  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      if (grid[r][c] === 1) {
        maxArea = Math.max(maxArea, dfs(r, c));
      }
    }
  }

  return maxArea;
}
```

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn max_area_of_island(mut grid: Vec<Vec<i32>>) -> i32 {
        let m = grid.len();
        let n = grid[0].len();
        let mut max_area = 0;

        for r in 0..m {
            for c in 0..n {
                if grid[r][c] == 1 {
                    let area = Self::dfs(&mut grid, r, c, m, n);
                    max_area = max_area.max(area);
                }
            }
        }

        max_area
    }

    fn dfs(grid: &mut Vec<Vec<i32>>, r: usize, c: usize, m: usize, n: usize) -> i32 {
        if grid[r][c] != 1 {
            return 0;
        }

        grid[r][c] = 0;
        let mut area = 1;

        let dirs: [(isize, isize); 4] = [(0, 1), (1, 0), (0, -1), (-1, 0)];
        for (dr, dc) in dirs {
            let nr = r as isize + dr;
            let nc = c as isize + dc;
            if nr >= 0 && nr < m as isize && nc >= 0 && nc < n as isize {
                area += Self::dfs(grid, nr as usize, nc as usize, m, n);
            }
        }

        area
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(m * n)` since each cell is visited at most once.
- Space Complexity: `O(m * n)` worst-case recursive call stack for fully connected grid.
