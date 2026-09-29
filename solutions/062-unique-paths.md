# 62. Unique Paths

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(n) rolling 1D array

## Rust Implementation
```rust
pub fn unique_paths(m: i32, n: i32) -> i32 {
    let mut row = vec![1; n as usize];
    for _ in 1..m {
        for j in 1..n as usize {
            row[j] += row[j - 1];
        }
    }
    row[(n - 1) as usize]
}
```
