# 209. Minimum Size Subarray Sum

## Problem Statement
Given an array of positive integers `nums` and a positive integer `target`, return the minimal length of a contiguous subarray `[numsl, numsl+1, ..., numsr-1, numsr]` of which the sum is greater than or equal to `target`. If there is no such subarray, return `0` instead.

---

## Algorithmic Strategy: Monotonic Window Shrinking

Since all elements are strictly positive (`nums[i] > 0`), the window sum grows monotonically as `right` expands and decreases monotonically as `left` advances. This permits a two-pointer sliding window operating in linear time.

---

## TypeScript Implementation

```typescript
export function minSubArrayLen(target: number, nums: number[]): number {
  let left = 0;
  let currentSum = 0;
  let minLength = Infinity;

  for (let right = 0; right < nums.length; right++) {
    currentSum += nums[right];

    while (currentSum >= target) {
      minLength = Math.min(minLength, right - left + 1);
      currentSum -= nums[left];
      left++;
    }
  }

  return minLength === Infinity ? 0 : minLength;
}
```

---

## Rust Implementation

```rust
pub fn min_sub_array_len(target: i32, nums: Vec<i32>) -> i32 {
    let mut left = 0;
    let mut current_sum = 0;
    let mut min_len = usize::MAX;

    for right in 0..nums.len() {
        current_sum += nums[right];

        while current_sum >= target {
            min_len = min_len.min(right - left + 1);
            current_sum -= nums[left];
            left += 1;
        }
    }

    if min_len == usize::MAX { 0 } else { min_len as i32 }
}
```

---

## Complexity Analysis

* **Time Complexity:** `O(N)` because both `left` and `right` traverse the array at most once.
* **Space Complexity:** `O(1)` auxiliary memory with zero dynamic allocations.
