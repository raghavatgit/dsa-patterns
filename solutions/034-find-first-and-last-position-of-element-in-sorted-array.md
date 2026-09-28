# 34. Find First and Last Position of Element in Sorted Array

## Complexity
- Time Complexity: O(log n)
- Space Complexity: O(1)

## Approach
Execute two independent binary searches: one biased towards the lower bound to locate the leftmost occurrence, and another biased towards the upper bound to locate the rightmost occurrence.

## Rust Implementation
```rust
pub fn search_range(nums: Vec<i32>, target: i32) -> Vec<i32> {
    fn find_bound(nums: &[i32], target: i32, is_first: bool) -> i32 {
        let mut left = 0;
        let mut right = nums.len() as i32 - 1;
        let mut bound = -1;

        while left <= right {
            let mid = left + (right - left) / 2;
            if nums[mid as usize] == target {
                bound = mid;
                if is_first {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else if nums[mid as usize] < target {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        bound
    }

    let first = find_bound(&nums, target, true);
    if first == -1 {
        return vec![-1, -1];
    }
    let last = find_bound(&nums, target, false);
    vec![first, last]
}
```

## TypeScript Implementation
```typescript
export function searchRange(nums: number[], target: number): number[] {
    const findBound = (isFirst: boolean): number => {
        let left = 0, right = nums.length - 1, bound = -1;
        while (left <= right) {
            const mid = Math.floor(left + (right - left) / 2);
            if (nums[mid] === target) {
                bound = mid;
                if (isFirst) right = mid - 1;
                else left = mid + 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return bound;
    };

    const first = findBound(true);
    if (first === -1) return [-1, -1];
    return [first, findBound(false)];
}
```
