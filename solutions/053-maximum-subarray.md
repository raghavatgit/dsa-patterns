# Problem: Maximum Subarray

## Problem Statement
Given an integer array `nums`, find the subarray with the largest sum, and return its sum.

## Intuition & Approach
Kadane's Algorithm:
1. Let `current_sum` be the maximum subarray sum ending at current index `i`.
2. At each step, either extend previous subarray or start fresh from current number:
   `current_sum = max(nums[i], current_sum + nums[i])`.
3. Update `max_so_far = max(max_so_far, current_sum)`.
4. Time Complexity: $O(N)$ single pass. Space Complexity: $O(1)$ scalar tracking.

## TypeScript Implementation

```typescript
export function maxSubArray(nums: number[]): number {
  let currentSum = nums[0];
  let maxSoFar = nums[0];

  for (let i = 1; i < nums.length; i++) {
    currentSum = Math.max(nums[i], currentSum + nums[i]);
    maxSoFar = Math.max(maxSoFar, currentSum);
  }

  return maxSoFar;
}
```

## Rust Implementation

```rust
pub fn max_sub_array(nums: Vec<i32>) -> i32 {
    let mut current_sum = nums[0];
    let mut max_so_far = nums[0];

    for &num in nums.iter().skip(1) {
        current_sum = num.max(current_sum + num);
        max_so_far = max_so_far.max(current_sum);
    }

    max_so_far
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_max_subarray() {
        assert_eq!(max_sub_array(vec![-2, 1, -3, 4, -1, 2, 1, -5, 4]), 6);
        assert_eq!(max_sub_array(vec![1]), 1);
        assert_eq!(max_sub_array(vec![5, 4, -1, 7, 8]), 23);
    }
}
```
