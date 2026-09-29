# 167. Two Sum II

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn two_sum(numbers: Vec<i32>, target: i32) -> Vec<i32> {
    let mut l = 0;
    let mut r = numbers.len() - 1;

    while l < r {
        let sum = numbers[l] + numbers[r];
        if sum == target {
            return vec![(l + 1) as i32, (r + 1) as i32];
        } else if sum < target {
            l += 1;
        } else {
            r -= 1;
        }
    }
    vec![]
}
```
