# 901. Online Stock Span

## Complexity
- Time Complexity: O(1) amortized per next call
- Space Complexity: O(n)

## Rust Implementation
```rust
pub struct StockSpanner {
    stack: Vec<(i32, i32)>, // (price, span)
}

impl StockSpanner {
    pub fn new() -> Self {
        StockSpanner { stack: Vec::new() }
    }

    pub fn next(&mut self, price: i32) -> i32 {
        let mut span = 1;
        while let Some(&(top_price, top_span)) = self.stack.last() {
            if top_price <= price {
                span += top_span;
                self.stack.pop();
            } else {
                break;
            }
        }
        self.stack.push((price, span));
        span
    }
}
```
