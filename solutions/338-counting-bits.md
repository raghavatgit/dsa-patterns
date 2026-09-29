# 338. Counting Bits

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn count_bits(n: i32) -> Vec<i32> {
    let n = n as usize;
    let mut dp = vec![0; n + 1];
    for i in 1..=n {
        dp[i] = dp[i >> 1] + ((i & 1) as i32);
    }
    dp
}
```
