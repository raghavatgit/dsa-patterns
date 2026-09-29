# 53. Maximum Subarray

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn max_sub_array(nums: Vec<i32>) -> i32 {
    let mut max_sum = nums[0];
    let mut curr_sum = nums[0];

    for &x in nums.iter().skip(1) {
        curr_sum = std::cmp::max(x, curr_sum + x);
        max_sum = std::cmp::max(max_sum, curr_sum);
    }

    max_sum
}
```
