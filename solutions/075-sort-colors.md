# 75. Sort Colors

## Problem Statement
Given an array `nums` with `n` objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with colors in the order red (`0`), white (`1`), and blue (`2`).

---

## Method Explanation
Edsger Dijkstra's Dutch National Flag 3-pointer partition:
- Maintain three pointers: `low = 0`, `mid = 0`, `high = n - 1`.
- Invariant:
  - `nums[0..low]` are all `0`.
  - `nums[low..mid]` are all `1`.
  - `nums[mid..high+1]` are unexplored.
  - `nums[high+1..n]` are all `2`.
- When `nums[mid] == 0`: swap with `low`, advance `low` and `mid`.
- When `nums[mid] == 1`: advance `mid`.
- When `nums[mid] == 2`: swap with `high`, decrement `high` (do not advance `mid`).

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn sort_colors(nums: &mut Vec<i32>) {
        if nums.is_empty() {
            return;
        }

        let mut low = 0;
        let mut mid = 0;
        let mut high = nums.len() - 1;

        while mid <= high {
            match nums[mid] {
                0 => {
                    nums.swap(low, mid);
                    low += 1;
                    mid += 1;
                }
                1 => {
                    mid += 1;
                }
                2 => {
                    nums.swap(mid, high);
                    if high == 0 {
                        break;
                    }
                    high -= 1;
                }
                _ => unreachable!(),
            }
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_sort_colors() {
        let mut nums = vec![2, 0, 2, 1, 1, 0];
        Solution::sort_colors(&mut nums);
        assert_eq!(nums, vec![0, 0, 1, 1, 2, 2]);
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(N)` single pass through the array.
- Space Complexity: `O(1)` in-place element swaps.
