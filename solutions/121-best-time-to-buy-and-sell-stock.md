# 121. Best Time to Buy and Sell Stock

## Complexity
- Time Complexity: O(n) single pass
- Space Complexity: O(1) auxiliary

## Rust Implementation
```rust
pub fn max_profit(prices: Vec<i32>) -> i32 {
    let mut min_price = i32::MAX;
    let mut max_prof = 0;
    for price in prices {
        if price < min_price {
            min_price = price;
        } else {
            max_prof = max_prof.max(price - min_price);
        }
    }
    max_prof
}
```

## TypeScript Implementation
```typescript
export function maxProfit(prices: number[]): number {
    let minPrice = Infinity;
    let maxProfit = 0;
    for (const price of prices) {
        if (price < minPrice) {
            minPrice = price;
        } else {
            maxProfit = Math.max(maxProfit, price - minPrice);
        }
    }
    return maxProfit;
}
```
