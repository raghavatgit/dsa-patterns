# 123. Best Time to Buy and Sell Stock III

## Problem Statement
Find the maximum profit you can achieve given `prices`, with at most two transactions.

---

## Method Explanation
Model the process using 4 state variables:
1. `buy1`: maximum balance after first buy.
2. `sell1`: maximum balance after first sell.
3. `buy2`: maximum balance after second buy.
4. `sell2`: maximum balance after second sell.

Transitions:
- `buy1 = max(buy1, -price)`
- `sell1 = max(sell1, buy1 + price)`
- `buy2 = max(buy2, sell1 - price)`
- `sell2 = max(sell2, buy2 + price)`

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn max_profit(prices: Vec<i32>) -> i32 {
        let mut buy1 = i32::MIN;
        let mut sell1 = 0;
        let mut buy2 = i32::MIN;
        let mut sell2 = 0;

        for price in prices {
            buy1 = buy1.max(-price);
            sell1 = sell1.max(buy1 + price);
            buy2 = buy2.max(sell1 - price);
            sell2 = sell2.max(buy2 + price);
        }

        sell2
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_stock_iii() {
        assert_eq!(Solution::max_profit(vec![3, 3, 5, 0, 0, 3, 1, 4]), 6);
        assert_eq!(Solution::max_profit(vec![1, 2, 3, 4, 5]), 4);
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(N)`.
- Space Complexity: `O(1)`.
