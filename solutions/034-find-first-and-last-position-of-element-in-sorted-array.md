# 34. Find First and Last Position of Element in Sorted Array

## Complexity
- Time Complexity: O(log n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn search_range(nums: Vec<i32>, target: i32) -> Vec<i32> {
    fn find_bound(nums: &[i32], target: i32, is_first: bool) -> i32 {
        let mut l = 0;
        let mut r = nums.len() as i32 - 1;
        let mut ans = -1;
        while l <= r {
            let m = l + (r - l) / 2;
            if nums[m as usize] == target {
                ans = m;
                if is_first { r = m - 1; } else { l = m + 1; }
            } else if nums[m as usize] < target {
                l = m + 1;
            } else {
                r = m - 1;
            }
        }
        ans
    }
    vec![find_bound(&nums, target, true), find_bound(&nums, target, false)]
}
```
