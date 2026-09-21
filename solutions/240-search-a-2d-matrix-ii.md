# Problem: Search a 2D Matrix II

## Problem Statement
Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:
- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

## Intuition & Approach
Top-Right Corner Pointer Elimination:
1. Start search from the top-right corner `(r = 0, c = n - 1)`:
   - If `matrix[r][c] == target`, return `true`.
   - If `matrix[r][c] > target`, the target cannot exist in the current column (all elements below are even larger). Eliminate column: `c--`.
   - If `matrix[r][c] < target`, the target cannot exist in the current row (all elements to the left are even smaller). Eliminate row: `r++`.
2. Each step eliminates an entire row or column.
3. Time Complexity: $O(M + N)$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function searchMatrixII(matrix: number[][], target: number): boolean {
  const m = matrix.length;
  if (m === 0) return false;
  const n = matrix[0].length;

  let r = 0;
  let c = n - 1;

  while (r < m && c >= 0) {
    const val = matrix[r][c];
    if (val === target) {
      return true;
    } else if (val > target) {
      c--;
    } else {
      r++;
    }
  }

  return false;
}
```
