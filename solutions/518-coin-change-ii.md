# 518. Coin Change II

## Complexity
- Time Complexity: O(coins.length * amount)
- Space Complexity: O(amount)

## Rust Implementation
```rust
pub fn change(amount: i32, coins: Vec<i32>) -> i32 {
    let a = amount as usize;
    let mut dp = vec![0; a + 1];
    dp[0] = 1;

    for coin in coins {
        let c = coin as usize;
        for i in c..=a {
            dp[i] += dp[i - c];
        }
    }

    dp[a]
}
```
