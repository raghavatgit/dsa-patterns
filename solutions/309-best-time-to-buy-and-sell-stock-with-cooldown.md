# 309. Best Time to Buy and Sell Stock with Cooldown

## Problem Statement
You are given an array `prices` where `prices[i]` is the price on day `i`. After you sell your stock, you cannot buy stock on the next day (i.e., 1-day cooldown). Find the maximum profit.

---

## Method Explanation
Three mutual states on day `i`:
1. `held`: holding a share. `held = max(held, rest - price)`
2. `sold`: sold today (triggers cooldown tomorrow). `sold = held + price`
3. `rest`: cooldown or idle. `rest = max(rest, prev_sold)`

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn max_profit(prices: Vec<i32>) -> i32 {
        if prices.is_empty() {
            return 0;
        }

        let mut held = -prices[0];
        let mut sold = 0;
        let mut rest = 0;

        for &price in prices.iter().skip(1) {
            let prev_sold = sold;
            sold = held + price;
            held = held.max(rest - price);
            rest = rest.max(prev_sold);
        }

        sold.max(rest)
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_cooldown() {
        assert_eq!(Solution::max_profit(vec![1, 2, 3, 0, 2]), 3);
        assert_eq!(Solution::max_profit(vec![1]), 0);
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(N)`.
- Space Complexity: `O(1)`.
