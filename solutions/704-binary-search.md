# 704. Binary Search

## Problem Statement
Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

Algorithm runtime complexity must be `O(log n)`.

---

## TypeScript Implementation

```typescript
export function search(nums: number[], target: number): number {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    const mid = left + Math.floor((right - left) / 2);
    const midVal = nums[mid];

    if (midVal === target) {
      return mid;
    } else if (midVal < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}
```

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn search(nums: Vec<i32>, target: i32) -> i32 {
        let mut left: usize = 0;
        if nums.is_empty() {
            return -1;
        }
        let mut right: usize = nums.len() - 1;

        while left <= right {
            let mid = left + (right - left) / 2;
            let val = nums[mid];

            if val == target {
                return mid as i32;
            } else if val < target {
                left = mid + 1;
            } else {
                if mid == 0 {
                    break;
                }
                right = mid - 1;
            }
        }

        -1
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(log n)` since the search space is halved every iteration.
- Space Complexity: `O(1)` auxiliary storage.
