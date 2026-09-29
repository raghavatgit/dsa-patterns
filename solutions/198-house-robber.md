# 198. House Robber

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn rob(nums: Vec<i32>) -> i32 {
    let mut rob1 = 0;
    let mut rob2 = 0;
    for n in nums {
        let temp = rob2.max(rob1 + n);
        rob1 = rob2;
        rob2 = temp;
    }
    rob2
}
```
