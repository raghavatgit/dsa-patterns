# 33. Search in Rotated Sorted Array

## Complexity
- Time Complexity: O(log n)
- Space Complexity: O(1)

## Invariant
At least one half of the array (left or right of mid) is guaranteed to be strictly sorted. We identify the sorted half and determine if the target falls within its bounds.

## Rust Implementation
```rust
pub fn search(nums: Vec<i32>, target: i32) -> i32 {
    let mut left = 0;
    let mut right = nums.len() as i32 - 1;

    while left <= right {
        let mid = left + (right - left) / 2;
        let mid_val = nums[mid as usize];

        if mid_val == target {
            return mid;
        }

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

## TypeScript Implementation
```typescript
export function search(nums: number[], target: number): number {
    let left = 0;
    let right = nums.length - 1;

    while (left <= right) {
        const mid = Math.floor(left + (right - left) / 2);
        if (nums[mid] === target) return mid;

        if (nums[left] <= nums[mid]) {
            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } else {
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
