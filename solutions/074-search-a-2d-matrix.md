# 74. Search a 2D Matrix

## Complexity
- Time Complexity: O(log(m * n))
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn search_matrix(matrix: Vec<Vec<i32>>, target: i32) -> bool {
    let m = matrix.len();
    let n = matrix[0].len();
    let mut left = 0;
    let mut right = (m * n) as i32 - 1;

    while left <= right {
        let mid = left + (right - left) / 2;
        let r = (mid as usize) / n;
        let c = (mid as usize) % n;
        let val = matrix[r][c];

        if val == target {
            return true;
        } else if val < target {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    false
}
```

## TypeScript Implementation
```typescript
export function searchMatrix(matrix: number[][], target: number): boolean {
    const m = matrix.length;
    const n = matrix[0].length;
    let left = 0, right = m * n - 1;

    while (left <= right) {
        const mid = Math.floor(left + (right - left) / 2);
        const r = Math.floor(mid / n);
        const c = mid % n;
        const val = matrix[r][c];

        if (val === target) return true;
        if (val < target) left = mid + 1;
        else right = mid - 1;
    }

    return false;
}
```
