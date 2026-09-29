# 279. Perfect Squares

## Complexity
- Time Complexity: O(n * sqrt(n))
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn num_squares(n: i32) -> i32 {
    let n = n as usize;
    let mut dp = vec![i32::MAX; n + 1];
    dp[0] = 0;

    for i in 1..=n {
        let mut s = 1;
        while s * s <= i {
            dp[i] = dp[i].min(dp[i - s * s] + 1);
            s += 1;
        }
    }
    dp[n]
}
```
