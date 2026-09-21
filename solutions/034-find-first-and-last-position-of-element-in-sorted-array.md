# Problem: Find First and Last Position of Element in Sorted Array

## Problem Statement
Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value. If `target` is not found in the array, return `[-1, -1]`. You must write an algorithm with $O(\log N)$ runtime complexity.

## Intuition & Approach
Dual Binary Search (Lower Bound & Upper Bound):
1. Helper function `findBound(isFirst)`:
   - When `nums[mid] == target`:
     - If searching for first index (`isFirst == true`): continue searching left `high = mid - 1` to find earlier occurrences.
     - If searching for last index (`isFirst == false`): continue searching right `low = mid + 1` to find later occurrences.
2. Time Complexity: $2 \times O(\log N) = O(\log N)$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function searchRange(nums: number[], target: number): number[] {
  function findBound(isFirst: boolean): number {
    let low = 0;
    let high = nums.length - 1;
    let bound = -1;

    while (low <= high) {
      const mid = low + Math.floor((high - low) / 2);
      if (nums[mid] === target) {
        bound = mid;
        if (isFirst) {
          high = mid - 1;
        } else {
          low = mid + 1;
        }
      } else if (nums[mid] < target) {
        low = mid + 1;
      } else {
        high = mid - 1;
      }
    }

    return bound;
  }

  return [findBound(true), findBound(false)];
}
```
