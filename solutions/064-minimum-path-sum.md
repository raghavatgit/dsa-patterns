# 64. Minimum Path Sum

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(1) in-place accumulation

## Rust Implementation
```rust
pub fn min_path_sum(mut grid: Vec<Vec<i32>>) -> i32 {
    let m = grid.len();
    let n = grid[0].len();

    for i in 1..m { grid[i][0] += grid[i - 1][0]; }
    for j in 1..n { grid[0][j] += grid[0][j - 1]; }

    for i in 1..m {
        for j in 1..n {
            grid[i][j] += grid[i - 1][j].min(grid[i][j - 1]);
        }
    }
    grid[m - 1][n - 1]
}
```
