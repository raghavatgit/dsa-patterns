# 122. Best Time to Buy and Sell Stock II

## Problem Statement
You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `i`-th day. On each day, you may decide to buy and/or sell the stock. You can only hold at most one share of the stock at any time. Return the maximum profit you can achieve.

---

## Method Explanation
Every continuous ascending segment can be decomposed into pairwise daily price differentials:
`prices[j] - prices[i] = (prices[j] - prices[j-1]) + ... + (prices[i+1] - prices[i])`.
Greedy strategy: sum all positive daily increments `max(0, prices[i] - prices[i-1])`.

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn max_profit(prices: Vec<i32>) -> i32 {
        let mut total_profit = 0;
        for i in 1..prices.len() {
            if prices[i] > prices[i - 1] {
                total_profit += prices[i] - prices[i - 1];
            }
        }
        total_profit
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_max_profit() {
        assert_eq!(Solution::max_profit(vec![7, 1, 5, 3, 6, 4]), 7);
        assert_eq!(Solution::max_profit(vec![1, 2, 3, 4, 5]), 4);
        assert_eq!(Solution::max_profit(vec![7, 6, 4, 3, 1]), 0);
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(N)` single linear pass.
- Space Complexity: `O(1)` auxiliary space.
