# 048. Rotate Image

## Problem Statement
You are given an `n x n` 2D matrix representing an image. Rotate the image by 90 degrees clockwise in-place.

---

## Mathematical Transformation
A 90-degree clockwise rotation decomposes into two clean matrix operations:
1. **Transpose Matrix:** Swap `matrix[i][j]` with `matrix[j][i]`.
2. **Reverse Rows:** Horizontally reverse each row vector.

---

## TypeScript Implementation

```typescript
export function rotate(matrix: number[][]): void {
  const n = matrix.length;

  // 1. Transpose
  for (let i = 0; i < n; i++) {
    for (let j = i + 1; j < n; j++) {
      const temp = matrix[i][j];
      matrix[i][j] = matrix[j][i];
      matrix[j][i] = temp;
    }
  }

  // 2. Reverse each row
  for (let i = 0; i < n; i++) {
    matrix[i].reverse();
  }
}
```

---

## Rust Implementation

```rust
pub fn rotate(matrix: &mut Vec<Vec<i32>>) {
    let n = matrix.len();

    // 1. Transpose
    for i in 0..n {
        for j in (i + 1)..n {
            let temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }

    // 2. Reverse each row
    for row in matrix.iter_mut() {
        row.reverse();
    }
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N^2) visiting each cell twice.
* **Space Complexity:** O(1) in-place auxiliary space.
