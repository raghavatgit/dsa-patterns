# 188. Best Time to Buy and Sell Stock IV

## Problem Statement
You are given an integer array `prices` and an integer `k`. Find the maximum profit with at most `k` transactions.

---

## Method Explanation
- If `k >= n / 2`, the problem reduces to unlimited transactions (Greedy solution from LeetCode 122).
- Otherwise, maintain arrays `buy[k + 1]` and `sell[k + 1]`:
  - `buy[t] = max(buy[t], sell[t - 1] - price)`
  - `sell[t] = max(sell[t], buy[t] + price)`

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn max_profit(k: i32, prices: Vec<i32>) -> i32 {
        let n = prices.len();
        if n == 0 || k == 0 {
            return 0;
        }

        let k = k as usize;
        if k >= n / 2 {
            let mut profit = 0;
            for i in 1..n {
                if prices[i] > prices[i - 1] {
                    profit += prices[i] - prices[i - 1];
                }
            }
            return profit;
        }

        let mut buy = vec![i32::MIN; k + 1];
        let mut sell = vec![0; k + 1];

        for price in prices {
            for t in 1..=k {
                buy[t] = buy[t].max(sell[t - 1] - price);
                sell[t] = sell[t].max(buy[t] + price);
            }
        }

        sell[k]
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_stock_iv() {
        assert_eq!(Solution::max_profit(2, vec![2, 4, 1]), 2);
        assert_eq!(Solution::max_profit(2, vec![3, 2, 6, 5, 0, 3]), 7);
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(N * K)`.
- Space Complexity: `O(K)`.
