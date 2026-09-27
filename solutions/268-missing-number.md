# 268. Missing Number

## Problem Statement
Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

---

## Gauss Sum Formula
Sum of numbers from 0 to n is `n * (n + 1) / 2`. Subtract sum of array to reveal missing number in O(N) time and O(1) space.

---

## TypeScript Implementation

```typescript
export function missingNumber(nums: number[]): number {
  const n = nums.length;
  const expectedSum = (n * (n + 1)) / 2;
  const actualSum = nums.reduce((acc, val) => acc + val, 0);
  return expectedSum - actualSum;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N).
* **Space Complexity:** O(1).
