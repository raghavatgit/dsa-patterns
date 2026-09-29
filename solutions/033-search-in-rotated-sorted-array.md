# 33. Search in Rotated Sorted Array

## Complexity
- Time Complexity: O(log n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn search(nums: Vec<i32>, target: i32) -> i32 {
    let mut left = 0;
    let mut right = nums.len() as i32 - 1;

    while left <= right {
        let mid = left + (right - left) / 2;
        let mid_val = nums[mid as usize];
        if mid_val == target { return mid; }

        if nums[left as usize] <= mid_val {
            if nums[left as usize] <= target && target < mid_val {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } else {
            if mid_val < target && target <= nums[right as usize] {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }
    -1
}
```
