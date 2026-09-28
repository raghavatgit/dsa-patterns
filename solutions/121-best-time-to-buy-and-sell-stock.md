# 121. Best Time to Buy and Sell Stock

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn max_profit(prices: Vec<i32>) -> i32 {
    let mut min_price = i32::MAX;
    let mut max_p = 0;

    for p in prices {
        if p < min_price {
            min_price = p;
        } else if p - min_price > max_p {
            max_p = p - min_price;
        }
    }

    max_p
}
```
