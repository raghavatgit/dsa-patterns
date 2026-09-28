# 240. Search a 2D Matrix II

## Complexity
- Time Complexity: O(m + n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn search_matrix(matrix: Vec<Vec<i32>>, target: i32) -> bool {
    let mut r = 0;
    let mut c = matrix[0].len() as i32 - 1;

    while (r as usize) < matrix.len() && c >= 0 {
        let val = matrix[r as usize][c as usize];
        if val == target {
            return true;
        } else if val > target {
            c -= 1;
        } else {
            r += 1;
        }
    }

    false
}
```

## TypeScript Implementation
```typescript
export function searchMatrix(matrix: number[][], target: number): boolean {
    let r = 0, c = matrix[0].length - 1;
    while (r < matrix.length && c >= 0) {
        const val = matrix[r][c];
        if (val === target) return true;
        if (val > target) c--;
        else r++;
    }
    return false;
}
```
