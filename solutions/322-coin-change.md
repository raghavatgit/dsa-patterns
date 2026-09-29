# 322. Coin Change

## Complexity
- Time Complexity: O(amount * len(coins))
- Space Complexity: O(amount)

## Rust Implementation
```rust
pub fn coin_change(coins: Vec<i32>, amount: i32) -> i32 {
    let amt = amount as usize;
    let mut dp = vec![amt + 1; amt + 1];
    dp[0] = 0;

    for i in 1..=amt {
        for &coin in &coins {
            let c = coin as usize;
            if c <= i {
                dp[i] = dp[i].min(dp[i - c] + 1);
            }
        }
    }

    if dp[amt] > amt { -1 } else { dp[amt] as i32 }
}
```

## TypeScript Implementation
```typescript
export function coinChange(coins: number[], amount: number): number {
    const dp = new Array(amount + 1).fill(amount + 1);
    dp[0] = 0;

    for (let i = 1; i <= amount; i++) {
        for (const coin of coins) {
            if (coin <= i) {
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
            }
        }
    }

    return dp[amount] > amount ? -1 : dp[amount];
}
```
