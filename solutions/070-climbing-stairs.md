# 70. Climbing Stairs

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn climb_stairs(n: i32) -> i32 {
    if n <= 2 { return n; }
    let mut prev2 = 1;
    let mut prev1 = 2;
    for _ in 3..=n {
        let curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }
    prev1
}
```
