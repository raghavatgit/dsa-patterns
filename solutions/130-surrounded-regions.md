# 130. Surrounded Regions

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(m * n)

## Rust Implementation
```rust
pub fn solve(board: &mut Vec<Vec<char>>) {
    let m = board.len();
    let n = board[0].len();

    fn dfs(b: &mut Vec<Vec<char>>, r: usize, c: usize, m: usize, n: usize) {
        if b[r][c] != 'O' { return; }
        b[r][c] = 'E';
        if r > 0 { dfs(b, r - 1, c, m, n); }
        if r + 1 < m { dfs(b, r + 1, c, m, n); }
        if c > 0 { dfs(b, r, c - 1, m, n); }
        if c + 1 < n { dfs(b, r, c + 1, m, n); }
    }

    for i in 0..m {
        dfs(board, i, 0, m, n);
        dfs(board, i, n - 1, m, n);
    }
    for j in 0..n {
        dfs(board, 0, j, m, n);
        dfs(board, m - 1, j, m, n);
    }

    for i in 0..m {
        for j in 0..n {
            if board[i][j] == 'O' { board[i][j] = 'X'; }
            else if board[i][j] == 'E' { board[i][j] = 'O'; }
        }
    }
}
```
