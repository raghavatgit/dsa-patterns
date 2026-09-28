# 62. Unique Paths

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn unique_paths(m: i32, n: i32) -> i32 {
    let n = n as usize;
    let mut dp = vec![1; n];

    for _ in 1..m {
        for j in 1..n {
            dp[j] += dp[j - 1];
        }
    }

    dp[n - 1]
}
```
