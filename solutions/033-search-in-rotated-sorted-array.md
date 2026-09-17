# Problem: Search in Rotated Sorted Array

## Problem Statement
Given an integer array `nums` sorted in ascending order (with distinct values) that has been rotated at an unknown pivot index, and a `target` value, return the index of `target` if it is in `nums`, or `-1` if it is not.

## Intuition & Approach
In any rotated sorted array, splitting at midpoint `mid` always divides the array into at least one strictly sorted half:
1. If `nums[left] <= nums[mid]`, the left half `[left, mid]` is strictly sorted:
   * If `nums[left] <= target < nums[mid]`, search the left half (`right = mid - 1`).
   * Otherwise, search the right half (`left = mid + 1`).
2. Otherwise, the right half `[mid, right]` is strictly sorted:
   * If `nums[mid] < target <= nums[right]`, search the right half (`left = mid + 1`).
   * Otherwise, search the left half (`right = mid - 1`).

## TypeScript Implementation

```typescript
export function search(nums: number[], target: number): number {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (nums[mid] === target) return mid;

    // Determine which half is sorted
    if (nums[left] <= nums[mid]) {
      // Left half is sorted
      if (nums[left] <= target && target < nums[mid]) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    } else {
      // Right half is sorted
      if (nums[mid] < target && target <= nums[right]) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
  }

  return -1;
}
```

## Rust Implementation

```rust
pub fn search(nums: &[i32], target: i32) -> i32 {
    let mut left = 0;
    let mut right = nums.len() as isize - 1;

    while left <= right {
        let mid = (left + right) / 2;
        let mid_val = nums[mid as usize];

        if mid_val == target {
            return mid as i32;
        }

        if nums[left as usize] <= mid_val {
            // Left half is sorted
            if nums[left as usize] <= target && target < mid_val {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } else {
            // Right half is sorted
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

## Complexity Analysis
* **Time Complexity:** O(log N) logarithmic binary search.
* **Space Complexity:** O(1) constant auxiliary space.
