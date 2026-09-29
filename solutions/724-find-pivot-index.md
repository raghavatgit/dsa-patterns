# 724. Find Pivot Index

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn pivot_index(nums: Vec<i32>) -> i32 {
    let total: i32 = nums.iter().sum();
    let mut left_sum = 0;
    for (i, &x) in nums.iter().enumerate() {
        if left_sum == total - left_sum - x {
            return i as i32;
        }
        left_sum += x;
    }
    -1
}
```

## TypeScript Implementation
```typescript
export function pivotIndex(nums: number[]): number {
    const total = nums.reduce((a, b) => a + b, 0);
    let leftSum = 0;
    for (let i = 0; i < nums.length; i++) {
        if (leftSum === total - leftSum - nums[i]) {
            return i;
        }
        leftSum += nums[i];
    }
    return -1;
}
```
