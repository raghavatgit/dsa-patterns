# 200. Number of Islands

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(m * n) recursion stack

## Rust Implementation
```rust
pub fn num_islands(mut grid: Vec<Vec<char>>) -> i32 {
    let m = grid.len();
    let n = grid[0].len();
    let mut count = 0;

    fn dfs(grid: &mut Vec<Vec<char>>, r: usize, c: usize, m: usize, n: usize) {
        if grid[r][c] != '1' { return; }
        grid[r][c] = '0';
        if r > 0 { dfs(grid, r - 1, c, m, n); }
        if r + 1 < m { dfs(grid, r + 1, c, m, n); }
        if c > 0 { dfs(grid, r, c - 1, m, n); }
        if c + 1 < n { dfs(grid, r, c + 1, m, n); }
    }

    for i in 0..m {
        for j in 0..n {
            if grid[i][j] == '1' {
                count += 1;
                dfs(&mut grid, i, j, m, n);
            }
        }
    }
    count
}
```
