# 309. Best Time to Buy and Sell Stock with Cooldown

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1) state variables

## Rust Implementation
```rust
pub fn max_profit(prices: Vec<i32>) -> i32 {
    let mut sold = 0;
    let mut hold = i32::MIN;
    let mut rest = 0;

    for p in prices {
        let prev_sold = sold;
        sold = hold + p;
        hold = hold.max(rest - p);
        rest = rest.max(prev_sold);
    }
    sold.max(rest)
}
```
