# Problem: Word Search

## Problem Statement
Given an `m x n` grid of characters `board` and a string `word`, return `true` if `word` exists in the grid. The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

## Intuition & Approach
In-Place Cell Flipping DFS:
1. Scan board: when `board[r][c] == word[0]`, initiate DFS.
2. DFS at `(r, c, k)`:
   - If $k == \text{word.length}$, complete word matched: return `true`.
   - Boundary checks: if $r < 0$ or $r \ge M$ or $c < 0$ or $c \ge N$ or `board[r][c] != word[k]`, return `false`.
   - Save character `tmp = board[r][c]`, mark visited in-place `board[r][c] = '#'`.
   - Recurse in 4 directions `(r + 1, c)`, `(r - 1, c)`, `(r, c + 1)`, `(r, c - 1)`.
   - Restore `board[r][c] = tmp` (backtrack).
3. Time Complexity: $O(M \times N \times 3^L)$ where $L = \text{len}(word)$. Space Complexity: $O(L)$ stack depth.

## TypeScript Implementation

```typescript
export function exist(board: string[][], word: string): boolean {
  const m = board.length;
  const n = board[0].length;

  function dfs(r: number, c: number, k: number): boolean {
    if (k === word.length) return true;
    if (r < 0 || r >= m || c < 0 || c >= n || board[r][c] !== word[k]) {
      return false;
    }

    const temp = board[r][c];
    board[r][c] = "#";

    const found =
      dfs(r + 1, c, k + 1) ||
      dfs(r - 1, c, k + 1) ||
      dfs(r, c + 1, k + 1) ||
      dfs(r, c - 1, k + 1);

    board[r][c] = temp;
    return found;
  }

  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      if (board[r][c] === word[0] && dfs(r, c, 0)) {
        return true;
      }
    }
  }

  return false;
}
```
