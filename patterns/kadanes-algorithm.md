# Kadane's Algorithm for Maximum Subarray Sum

## Concept
Kadane's algorithm solves the Maximum Subarray Problem in linear O(N) time with O(1) space. At each index `i`, the algorithm decides whether to extend the existing contiguous subarray sum or start a fresh subarray at `nums[i]`:

```text
current_max = max(nums[i], current_max + nums[i])
global_max  = max(global_max, current_max)
```

## TypeScript Implementation

```typescript
export function maxSubArray(nums: number[]): number {
  if (nums.length === 0) {
    throw new Error("Input array must contain at least one element");
  }

  let currentMax = nums[0];
  let globalMax = nums[0];

  for (let i = 1; i < nums.length; i++) {
    // Choose between extending the subarray or starting anew at nums[i]
    currentMax = Math.max(nums[i], currentMax + nums[i]);
    globalMax = Math.max(globalMax, currentMax);
  }

  return globalMax;
}
```

## Rust Implementation

```rust
pub fn max_sub_array(nums: &[i32]) -> Result<i32, &'static str> {
    if nums.is_empty() {
        return Err("Input slice must contain at least one element");
    }

    let mut current_max = nums[0];
    let mut global_max = nums[0];

    for &val in &nums[1..] {
        // Evaluate dynamic programming transition invariant
        current_max = val.max(current_max.saturating_add(val));
        global_max = global_max.max(current_max);
    }

    Ok(global_max)
}
```

## Complexity Analysis

* **Time Complexity:** O(N) single-pass iteration over the array.
* **Space Complexity:** O(1) auxiliary variables for state tracking.
* **Negative-Only Arrays:** Correctly initializes with `nums[0]` rather than `0`, returning the largest single negative element if all numbers are negative.
