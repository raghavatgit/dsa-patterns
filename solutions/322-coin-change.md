# 322. Coin Change

## Complexity
- Time Complexity: O(amount * n)
- Space Complexity: O(amount)

## Rust Implementation
```rust
pub fn coin_change(coins: Vec<i32>, amount: i32) -> i32 {
    let a = amount as usize;
    let mut dp = vec![amount + 1; a + 1];
    dp[0] = 0;

    for i in 1..=a {
        for &coin in &coins {
            if (coin as usize) <= i {
                dp[i] = std::cmp::min(dp[i], dp[i - coin as usize] + 1);
            }
        }
    }

    if dp[a] > amount { -1 } else { dp[a] }
}
```
