# 137. Single Number II

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn single_number(nums: Vec<i32>) -> i32 {
    let mut ones = 0;
    let mut twos = 0;

    for x in nums {
        ones = (ones ^ x) & !twos;
        twos = (twos ^ x) & !ones;
    }

    ones
}
```
