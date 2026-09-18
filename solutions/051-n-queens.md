# Problem: N-Queens (Bitmask Backtracking)

## Problem Statement
The $n$-queens puzzle is the problem of placing $n$ queens on an $n \times n$ chessboard such that no two queens attack each other. Return all distinct solutions to the $n$-queens puzzle.

## Intuition & Approach
Bitmask Constraint Propagation:
1. A queen at row `r` and column `c` attacks:
   - Column `c`
   - Major diagonal `r - c` (normalized as `r - c + (n - 1)`)
   - Minor diagonal `r + c`
2. Instead of arrays or hash sets, we use 3 bitmasks (`cols`, `diags1`, `diags2`):
   - Check if a column or diagonal is occupied with bitwise AND `(mask & (1 << bit)) != 0` in $O(1)$ time.
   - Set flags with bitwise OR, clear with bitwise XOR on backtracking.
3. This achieves maximum cache locality and eliminates heap allocations during tree exploration.
4. Time Complexity: $O(N!)$ upper bound pruned aggressively. Space Complexity: $O(N)$ recursion depth.

## TypeScript Implementation

```typescript
export function solveNQueens(n: number): string[][] {
  const results: string[][] = [];
  const board: number[] = new Array(n).fill(-1); // board[row] = col

  function backtrack(row: number, cols: number, diags1: number, diags2: number) {
    if (row === n) {
      const solution: string[] = [];
      for (let r = 0; r < n; r++) {
        const c = board[r];
        solution.push(".".repeat(c) + "Q" + ".".repeat(n - c - 1));
      }
      results.push(solution);
      return;
    }

    // Available positions for row: inverted bitmask of all attacking lines
    let available = ((1 << n) - 1) & ~(cols | diags1 | diags2);

    while (available > 0) {
      // Extract lowest set bit
      const bit = available & -available;
      const col = Math.log2(bit);

      board[row] = col;
      backtrack(row + 1, cols | bit, (diags1 | bit) << 1, (diags2 | bit) >> 1);
      board[row] = -1;

      available &= available - 1; // Clear lowest set bit
    }
  }

  backtrack(0, 0, 0, 0);
  return results;
}
```
