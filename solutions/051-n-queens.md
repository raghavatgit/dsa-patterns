# 51. N-Queens

## Complexity
- Time Complexity: O(N!)
- Space Complexity: O(N)

## TypeScript Implementation
```typescript
export function solveNQueens(n: number): string[][] {
    const res: string[][] = [];
    const cols = new Set<number>();
    const diag1 = new Set<number>(); // r - c
    const diag2 = new Set<number>(); // r + c
    const board = Array.from({ length: n }, () => new Array(n).fill('.'));

    const backtrack = (r: number) => {
        if (r === n) {
            res.push(board.map(row => row.join('')));
            return;
        }
        for (let c = 0; c < n; c++) {
            if (cols.has(c) || diag1.has(r - c) || diag2.has(r + c)) continue;
            cols.add(c); diag1.add(r - c); diag2.add(r + c);
            board[r][c] = 'Q';
            backtrack(r + 1);
            board[r][c] = '.';
            cols.delete(c); diag1.delete(r - c); diag2.delete(r + c);
        }
    };

    backtrack(0);
    return res;
}
```
