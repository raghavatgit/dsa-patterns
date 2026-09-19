# Problem: Coin Change

## Problem Statement
You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money. Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

## Intuition & Approach
Bottom-Up Dynamic Programming (Unbounded Knapsack):
1. Let `dp[i]` be the minimum number of coins required to make amount `i`.
2. Initialize array of size `amount + 1` filled with infinity (`amount + 1`), with base case `dp[0] = 0`.
3. For each target sub-amount $i$ from 1 to `amount`:
   - For each coin $c \in \text{coins}$:
     - If $i - c \ge 0$: `dp[i] = min(dp[i], 1 + dp[i - c])`.
4. If `dp[amount] > amount`, target is unreachable: return `-1`.
5. Time Complexity: $O(N \times \text{amount})$ where $N = \text{len}(coins)$. Space Complexity: $O(\text{amount})$.

## TypeScript Implementation

```typescript
export function coinChange(coins: number[], amount: number): number {
  const dp: number[] = new Array(amount + 1).fill(amount + 1);
  dp[0] = 0;

  for (let i = 1; i <= amount; i++) {
    for (const coin of coins) {
      if (i - coin >= 0) {
        dp[i] = Math.min(dp[i], 1 + dp[i - coin]);
      }
    }
  }

  return dp[amount] > amount ? -1 : dp[amount];
}
```

## Rust Implementation

```rust
pub fn coin_change(coins: Vec<i32>, amount: i32) -> i32 {
    let amt = amount as usize;
    let mut dp = vec![amount + 1; amt + 1];
    dp[0] = 0;

    for i in 1..=amt {
        for &coin in &coins {
            let c = coin as usize;
            if i >= c {
                dp[i] = dp[i].min(1 + dp[i - c]);
            }
        }
    }

    if dp[amt] > amount { -1 } else { dp[amt] }
}
```
