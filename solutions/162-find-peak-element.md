# 162. Find Peak Element

## Complexity
- Time Complexity: O(log n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn find_peak_element(nums: Vec<i32>) -> i32 {
    let mut left = 0;
    let mut right = nums.len() - 1;

    while left < right {
        let mid = left + (right - left) / 2;
        if nums[mid] < nums[mid + 1] {
            left = mid + 1;
        } else {
            right = mid;
        }
    }

    left as i32
}
```

## TypeScript Implementation
```typescript
export function findPeakElement(nums: number[]): number {
    let left = 0, right = nums.length - 1;
    while (left < right) {
        const mid = Math.floor(left + (right - left) / 2);
        if (nums[mid] < nums[mid + 1]) left = mid + 1;
        else right = mid;
    }
    return left;
}
```
