# Problem: Majority Element

## Problem Statement
Given an array `nums` of size `n`, return the majority element. The majority element is the element that appears more than $\lfloor n / 2 \rfloor$ times. You may assume that the majority element always exists in the array.

## Intuition & Approach
Boyer-Moore Majority Voting Algorithm:
1. Maintain a candidate `candidate` and a vote counter `count = 0`.
2. For each element `x`:
   - If `count == 0`, assign `candidate = x` and `count = 1`.
   - Else if `x == candidate`, increment `count++`.
   - Else decrement `count--`.
3. Because the majority element appears $> N / 2$ times, its votes exceed the sum of all other elements combined.
4. Time Complexity: Strict $O(N)$ single pass. Space Complexity: $O(1)$ variables.

## TypeScript Implementation

```typescript
export function majorityElement(nums: number[]): number {
  let candidate = nums[0];
  let count = 0;

  for (const num of nums) {
    if (count === 0) {
      candidate = num;
      count = 1;
    } else if (num === candidate) {
      count++;
    } else {
      count--;
    }
  }

  return candidate;
}
```

## Rust Implementation

```rust
pub fn majority_element(nums: Vec<i32>) -> i32 {
    let mut candidate = nums[0];
    let mut count = 0;

    for num in nums {
        if count == 0 {
            candidate = num;
            count = 1;
        } else if num == candidate {
            count += 1;
        } else {
            count -= 1;
        }
    }

    candidate
}
```
