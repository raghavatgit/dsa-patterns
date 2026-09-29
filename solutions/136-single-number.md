# 136. Single Number

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn single_number(nums: Vec<i32>) -> i32 {
    nums.into_iter().fold(0, |acc, x| acc ^ x)
}
```
