# 122. Best Time to Buy and Sell Stock II

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn max_profit(prices: Vec<i32>) -> i32 {
    let mut total = 0;
    for i in 1..prices.len() {
        if prices[i] > prices[i - 1] {
            total += prices[i] - prices[i - 1];
        }
    }
    total
}
```

## TypeScript Implementation
```typescript
export function maxProfit(prices: number[]): number {
    let total = 0;
    for (let i = 1; i < prices.length; i++) {
        if (prices[i] > prices[i - 1]) {
            total += prices[i] - prices[i - 1];
        }
    }
    return total;
}
```
