# 70. Climbing Stairs

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn climb_stairs(n: i32) -> i32 {
    if n <= 2 { return n; }
    let mut prev = 1;
    let mut curr = 2;
    for _ in 3..=n {
        let nxt = prev + curr;
        prev = curr;
        curr = nxt;
    }
    curr
}
```
