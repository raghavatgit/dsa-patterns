# Problem: Maximum Product Subarray

## Problem Statement
Given an integer array `nums`, find a subarray that has the largest product, and return the product.

## Intuition & Approach
Dual Min/Max Dynamic Programming:
1. Because multiplying by a negative number turns a minimum product into a potential maximum product, we must track both `curr_max` and `curr_min`.
2. For each number `x`:
   - If $x < 0$, swap `curr_max` and `curr_min`.
   - Update:
     `curr_max = max(x, curr_max * x)`
     `curr_min = min(x, curr_min * x)`
   - Update `global_max = max(global_max, curr_max)`.
3. Time Complexity: $O(N)$ single pass. Space Complexity: $O(1)$ auxiliary variables.

## TypeScript Implementation

```typescript
export function maxProduct(nums: number[]): number {
  let currMax = nums[0];
  let currMin = nums[0];
  let globalMax = nums[0];

  for (let i = 1; i < nums.length; i++) {
    const num = nums[i];

    if (num < 0) {
      const temp = currMax;
      currMax = currMin;
      currMin = temp;
    }

    currMax = Math.max(num, currMax * num);
    currMin = Math.min(num, currMin * num);

    globalMax = Math.max(globalMax, currMax);
  }

  return globalMax;
}
```

## Rust Implementation

```rust
pub fn max_product(nums: Vec<i32>) -> i32 {
    let mut curr_max = nums[0];
    let mut curr_min = nums[0];
    let mut global_max = nums[0];

    for &num in nums.iter().skip(1) {
        if num < 0 {
            std::mem::swap(&mut curr_max, &mut curr_min);
        }

        curr_max = num.max(curr_max * num);
        curr_min = num.min(curr_min * num);

        global_max = global_max.max(curr_max);
    }

    global_max
}
```
