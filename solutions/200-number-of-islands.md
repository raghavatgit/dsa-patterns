# Problem: Number of Islands

## Problem Statement
Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

## Intuition & Approach
Traverse each cell `(r, c)`. When land `'1'` is encountered:
1. Increment island counter.
2. Initiate Depth-First Search (DFS) to traverse all 4-directional connected land cells.
3. Sink visited land cells in-place to `'0'` to avoid re-visitation without extra memory.

## TypeScript Implementation

```typescript
export function numIslands(grid: string[][]): number {
  if (grid.length === 0) return 0;

  const rows = grid.length;
  const cols = grid[0].length;
  let count = 0;

  function dfs(r: number, c: number) {
    if (r < 0 || r >= rows || c < 0 || c >= cols || grid[r][c] !== '1') {
      return;
    }

    grid[r][c] = '0'; // Sink land cell

    dfs(r - 1, c); // Up
    dfs(r + 1, c); // Down
    dfs(r, c - 1); // Left
    dfs(r, c + 1); // Right
  }

  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === '1') {
        count++;
        dfs(r, c);
      }
    }
  }

  return count;
}
```

## Rust Implementation

```rust
pub fn num_islands(mut grid: Vec<Vec<char>>) -> i32 {
    if grid.is_empty() {
        return 0;
    }

    let rows = grid.len();
    let cols = grid[0].len();
    let mut count = 0;

    fn dfs(grid: &mut [Vec<char>], r: usize, c: usize, rows: usize, cols: usize) {
        grid[r][c] = '0';

        let directions = [(-1, 0), (1, 0), (0, -1), (0, 1)];
        for (dr, dc) in directions {
            let nr = r as isize + dr;
            let nc = c as isize + dc;

            if nr >= 0 && nr < rows as isize && nc >= 0 && nc < cols as isize {
                let ur = nr as usize;
                let uc = nc as usize;
                if grid[ur][uc] == '1' {
                    dfs(grid, ur, uc, rows, cols);
                }
            }
        }
    }

    for r in 0..rows {
        for c in 0..cols {
            if grid[r][c] == '1' {
                count += 1;
                dfs(&mut grid, r, c, rows, cols);
            }
        }
    }

    count
}
```

## Complexity Analysis
* **Time Complexity:** O(M * N) where every cell is visited at most twice.
* **Space Complexity:** O(M * N) worst case recursion stack depth for complete land grids.
