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
        let val = matrix[(mid as usize) / n][(mid as usize) % n];
        if val == target { return true; }
        else if val < target { left = mid + 1; }
        else { right = mid - 1; }
    }
    false
}
```
