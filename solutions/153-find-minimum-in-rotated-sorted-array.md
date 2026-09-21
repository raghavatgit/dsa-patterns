# Problem: Find Minimum in Rotated Sorted Array

## Problem Statement
Suppose an array of length `n` sorted in ascending order is rotated between 1 and `n` times. Given the sorted rotated array `nums` of unique elements, return the minimum element of this array. You must write an algorithm that runs in $O(\log N)$ time.

## Intuition & Approach
Binary Search Inflection Point:
1. If `nums[low] < nums[high]`, the active subarray is completely sorted: `nums[low]` is the minimum.
2. Calculate `mid = low + (high - low) / 2`.
3. Compare `nums[mid]` against `nums[high]`:
   - If `nums[mid] > nums[high]`, the minimum (inflection point) must lie to the right: `low = mid + 1`.
   - If `nums[mid] <= nums[high]`, the minimum lies at or to the left of `mid`: `high = mid`.
4. Loop terminates when `low == high`, pointing to the minimum element.
5. Time Complexity: $O(\log N)$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function findMin(nums: number[]): number {
  let low = 0;
  let high = nums.length - 1;

  while (low < high) {
    if (nums[low] < nums[high]) {
      return nums[low];
    }

    const mid = low + Math.floor((high - low) / 2);
    if (nums[mid] > nums[high]) {
      low = mid + 1;
    } else {
      high = mid;
    }
  }

  return nums[low];
}
```

## Rust Implementation

```rust
pub fn find_min(nums: Vec<i32>) -> i32 {
    let mut low = 0;
    let mut high = nums.len() - 1;

    while low < high {
        if nums[low] < nums[high] {
            return nums[low];
        }

        let mid = low + (high - low) / 2;
        if nums[mid] > nums[high] {
            low = mid + 1;
        } else {
            high = mid;
        }
    }

    nums[low]
}
```
