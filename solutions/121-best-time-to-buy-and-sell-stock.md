# Problem: Best Time to Buy and Sell Stock

## Problem Statement
You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`-th day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve. If you cannot achieve any profit, return `0`.

## Intuition & Approach
Maintain a running minimum price observed so far (`min_price`). At each day `i`:
1. Calculate potential profit if sold today: `prices[i] - min_price`.
2. Update `max_profit` if potential profit exceeds it.
3. Update `min_price = min(min_price, prices[i])`.

## TypeScript Implementation

```typescript
export function maxProfit(prices: number[]): number {
  let minPrice = Infinity;
  let maxProfit = 0;

  for (let i = 0; i < prices.length; i++) {
    if (prices[i] < minPrice) {
      minPrice = prices[i];
    } else if (prices[i] - minPrice > maxProfit) {
      maxProfit = prices[i] - minPrice;
    }
  }

  return maxProfit;
}
```

## Rust Implementation

```rust
pub fn max_profit(prices: &[i32]) -> i32 {
    let mut min_price = i32::MAX;
    let mut max_profit = 0;

    for &price in prices {
        if price < min_price {
            min_price = price;
        } else {
            max_profit = max_profit.max(price - min_price);
        }
    }

    max_profit
}
```

## Complexity Analysis
* **Time Complexity:** O(N) single-pass iteration.
* **Space Complexity:** O(1) constant auxiliary space.
