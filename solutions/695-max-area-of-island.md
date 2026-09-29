# 695. Max Area of Island

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(m * n)

## Rust Implementation
```rust
pub fn max_area_of_island(mut grid: Vec<Vec<i32>>) -> i32 {
    let m = grid.len();
    let n = grid[0].len();
    let mut max_area = 0;

    fn dfs(grid: &mut Vec<Vec<i32>>, r: usize, c: usize, m: usize, n: usize) -> i32 {
        if grid[r][c] != 1 { return 0; }
        grid[r][c] = 0;
        let mut area = 1;
        if r > 0 { area += dfs(grid, r - 1, c, m, n); }
        if r + 1 < m { area += dfs(grid, r + 1, c, m, n); }
        if c > 0 { area += dfs(grid, r, c - 1, m, n); }
        if c + 1 < n { area += dfs(grid, r, c + 1, m, n); }
        area
    }

    for i in 0..m {
        for j in 0..n {
            if grid[i][j] == 1 {
                max_area = max_area.max(dfs(&mut grid, i, j, m, n));
            }
        }
    }
    max_area
}
```
