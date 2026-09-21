# Problem: Search a 2D Matrix

## Problem Statement
You are given an `m x n` integer matrix `matrix` with the following two properties:
- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.
Given an integer `target`, return `true` if `target` is in `matrix` or `false` otherwise. You must write a solution in $O(\log(m \times n))$ time complexity.

## Intuition & Approach
Virtual 1D Flattened Binary Search:
1. Since each row connects sequentially to the next, the entire matrix can be treated as a single sorted array of length $M \times N$.
2. Binary search interval: `low = 0`, `high = m * n - 1`.
3. For midpoint index `mid`:
   - Row coordinate: `r = Math.floor(mid / n)`
   - Column coordinate: `c = mid % n`
4. Compare `matrix[r][c]` against `target` and adjust binary search boundaries accordingly.
5. Time Complexity: Strict $O(\log(M \times N))$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function searchMatrix(matrix: number[][], target: number): boolean {
  const m = matrix.length;
  if (m === 0) return false;
  const n = matrix[0].length;
  if (n === 0) return false;

  let low = 0;
  let high = m * n - 1;

  while (low <= high) {
    const mid = low + Math.floor((high - low) / 2);
    const r = Math.floor(mid / n);
    const c = mid % n;
    const val = matrix[r][c];

    if (val === target) {
      return true;
    } else if (val < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return false;
}
```

## Rust Implementation

```rust
pub fn search_matrix(matrix: Vec<Vec<i32>>, target: i32) -> bool {
    let m = matrix.len();
    if m == 0 { return false; }
    let n = matrix[0].len();
    if n == 0 { return false; }

    let mut low = 0;
    let mut high = (m * n) as i32 - 1;

    while low <= high {
        let mid = low + (high - low) / 2;
        let r = (mid as usize) / n;
        let c = (mid as usize) % n;
        let val = matrix[r][c];

        if val == target {
            return true;
        } else if val < target {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }

    false
}
```
