# 79. Word Search

## Complexity
- Time Complexity: O(m * n * 3^L)
- Space Complexity: O(L)

## Rust Implementation
```rust
pub fn exist(mut board: Vec<Vec<char>>, word: String) -> bool {
    let m = board.len();
    let n = board[0].len();
    let chars: Vec<char> = word.chars().collect();

    fn dfs(board: &mut Vec<Vec<char>>, r: usize, c: usize, idx: usize, word: &[char]) -> bool {
        if idx == word.len() { return true; }
        if board[r][c] != word[idx] { return false; }
        if idx == word.len() - 1 { return true; }

        let temp = board[r][c];
        board[r][c] = '#';

        let m = board.len();
        let n = board[0].len();
        let mut found = false;

        if r > 0 && dfs(board, r - 1, c, idx + 1, word) { found = true; }
        if !found && r + 1 < m && dfs(board, r + 1, c, idx + 1, word) { found = true; }
        if !found && c > 0 && dfs(board, r, c - 1, idx + 1, word) { found = true; }
        if !found && c + 1 < n && dfs(board, r, c + 1, idx + 1, word) { found = true; }

        board[r][c] = temp;
        found
    }

    for i in 0..m {
        for j in 0..n {
            if board[i][j] == chars[0] && dfs(&mut board, i, j, 0, &chars) {
                return true;
            }
        }
    }

    false
}
```
