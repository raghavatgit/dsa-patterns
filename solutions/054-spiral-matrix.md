# 054. Spiral Matrix

## Problem Statement
Given an `m x n` matrix, return all elements of the matrix in spiral order.

---

## Boundary Tracking Technique
Track four dynamic boundaries: `top`, `bottom`, `left`, `right`. Traverse right along `top`, down along `right`, left along `bottom`, and up along `left`, contracting boundaries after each pass.

---

## TypeScript Implementation

```typescript
export function spiralOrder(matrix: number[][]): number[] {
  if (matrix.length === 0) return [];
  const result: number[] = [];
  let top = 0, bottom = matrix.length - 1;
  let left = 0, right = matrix[0].length - 1;

  while (top <= bottom && left <= right) {
    for (let c = left; c <= right; c++) result.push(matrix[top][c]);
    top++;

    for (let r = top; r <= bottom; r++) result.push(matrix[r][right]);
    right--;

    if (top <= bottom) {
      for (let c = right; c >= left; c--) result.push(matrix[bottom][c]);
      bottom--;
    }

    if (left <= right) {
      for (let r = bottom; r >= top; r--) result.push(matrix[r][left]);
      left++;
    }
  }

  return result;
}
```

---

## Rust Implementation

```rust
pub fn spiral_order(matrix: Vec<Vec<i32>>) -> Vec<i32> {
    if matrix.is_empty() {
        return vec![];
    }

    let mut result = Vec::with_capacity(matrix.len() * matrix[0].len());
    let mut top = 0;
    let mut bottom = matrix.len() as i32 - 1;
    let mut left = 0;
    let mut right = matrix[0].len() as i32 - 1;

    while top <= bottom && left <= right {
        for c in left..=right {
            result.push(matrix[top as usize][c as usize]);
        }
        top += 1;

        for r in top..=bottom {
            result.push(matrix[r as usize][right as usize]);
        }
        right -= 1;

        if top <= bottom {
            for c in (left..=right).rev() {
                result.push(matrix[bottom as usize][c as usize]);
            }
            bottom -= 1;
        }

        if left <= right {
            for r in (top..=bottom).rev() {
                result.push(matrix[r as usize][left as usize]);
            }
            left += 1;
        }
    }

    result
}
```

---

## Complexity Analysis
* **Time Complexity:** O(M * N) every element visited once.
* **Space Complexity:** O(1) auxiliary space beyond the output vector.
