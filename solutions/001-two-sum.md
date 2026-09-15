# Problem: Two Sum

## Problem Statement
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`. You may assume that each input has exactly one solution, and you may not use the same element twice.

## Intuition & Approach
Instead of checking all pairs in O(N^2) time, use a hash map to store each number's index as we iterate. For each element `nums[i]`, compute its complement: `target - nums[i]`. If the complement already exists in the map, return the stored index and `i`.

## TypeScript Implementation

```typescript
export function twoSum(nums: number[], target: number): [number, number] {
  const map = new Map<number, number>();

  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (map.has(complement)) {
      return [map.get(complement)!, i];
    }
    map.set(nums[i], i);
  }

  throw new Error("No two sum solution found");
}
```

## Rust Implementation

```rust
use std::collections::HashMap;

pub fn two_sum(nums: &[i32], target: i32) -> Option<(usize, usize)> {
    let mut map = HashMap::with_capacity(nums.len());

    for (i, &num) in nums.iter().enumerate() {
        let complement = target - num;
        if let Some(&prev_idx) = map.get(&complement) {
            return Some((prev_idx, i));
        }
        map.insert(num, i);
    }

    None
}
```

## Complexity Analysis
* **Time Complexity:** O(N) single-pass traversal with O(1) hash map operations.
* **Space Complexity:** O(N) auxiliary memory for hash map storage.
