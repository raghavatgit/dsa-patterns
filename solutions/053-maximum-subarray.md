# Problem: Maximum Subarray

## Problem Statement
Given an integer array `nums`, find the subarray with the largest sum, and return its sum.

## Intuition & Approach
Kadane's Algorithm maintains a running local maximum. At each element `nums[i]`, evaluate whether to extend the previous running subarray sum or start a new contiguous subarray beginning at `nums[i]`:
`current_max = max(nums[i], current_max + nums[i])`
`global_max = max(global_max, current_max)`

## Rust Implementation

```rust
pub fn max_sub_array(nums: &[i32]) -> i32 {
    let mut current_max = nums[0];
    let mut global_max = nums[0];

    for &val in &nums[1..] {
        current_max = val.max(current_max + val);
        global_max = global_max.max(current_max);
    }

    global_max
}
```

## Complexity Analysis
* **Time Complexity:** O(N) single-pass iteration.
* **Space Complexity:** O(1) constant auxiliary space.
