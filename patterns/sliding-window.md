# Sliding Window Pattern

## Concept
The sliding window technique avoids redundant inner loops when calculating properties of contiguous subarrays or substrings by expanding a right boundary and contracting a left boundary.

## TypeScript Implementation

```typescript
export function maxSubarraySum(nums: number[], k: number): number {
  if (nums.length < k) return 0;

  let currentSum = 0;
  for (let i = 0; i < k; i++) {
    currentSum += nums[i];
  }

  let maxSum = currentSum;
  for (let i = k; i < nums.length; i++) {
    currentSum += nums[i] - nums[i - k];
    if (currentSum > maxSum) maxSum = currentSum;
  }

  return maxSum;
}
```

## Rust Implementation

```rust
pub fn max_subarray_sum(nums: &[i32], k: usize) -> Option<i32> {
    if nums.len() < k || k == 0 {
        return None;
    }

    let mut current_sum: i32 = nums[..k].iter().sum();
    let mut max_sum = current_sum;

    for i in k..nums.len() {
        current_sum += nums[i] - nums[i - k];
        if current_sum > max_sum {
            max_sum = current_sum;
        }
    }

    Some(max_sum)
}
```
