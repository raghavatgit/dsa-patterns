# 73. Set Matrix Zeroes

## Problem Statement
Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`s in-place.

---

## Method Explanation
To achieve `O(1)` additional memory:
1. Use the first row `matrix[0][..]` and first column `matrix[..][0]` as marker arrays.
2. Maintain two flags: `first_row_has_zero` and `first_col_has_zero`.
3. Scan the remainder of the matrix `matrix[1..m][1..n]`: if `matrix[i][j] == 0`, set `matrix[i][0] = 0` and `matrix[0][j] = 0`.
4. Fill inner cells based on the markers.
5. Zero out the first row/column if their flags were set.

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn set_zeroes(matrix: &mut Vec<Vec<i32>>) {
        let m = matrix.len();
        let n = matrix[0].len();
        let mut first_row_zero = false;
        let mut first_col_zero = false;

        for r in 0..m {
            if matrix[r][0] == 0 {
                first_col_zero = true;
                break;
            }
        }

        for c in 0..n {
            if matrix[0][c] == 0 {
                first_row_zero = true;
                break;
            }
        }

        for r in 1..m {
            for c in 1..n {
                if matrix[r][c] == 0 {
                    matrix[r][0] = 0;
                    matrix[0][c] = 0;
                }
            }
        }

        for r in 1..m {
            for c in 1..n {
                if matrix[r][0] == 0 || matrix[0][c] == 0 {
                    matrix[r][c] = 0;
                }
            }
        }

        if first_col_zero {
            for r in 0..m {
                matrix[r][0] = 0;
            }
        }

        if first_row_zero {
            for c in 0..n {
                matrix[0][c] = 0;
            }
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_set_zeroes() {
        let mut mat = vec![vec![1, 1, 1], vec![1, 0, 1], vec![1, 1, 1]];
        Solution::set_zeroes(&mut mat);
        assert_eq!(mat, vec![vec![1, 0, 1], vec![0, 0, 0], vec![1, 0, 1]]);
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(M * N)` where `M` is rows and `N` is columns.
- Space Complexity: `O(1)` strictly constant extra space.
