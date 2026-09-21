# Problem: Find Peak Element

## Problem Statement
A peak element is an element that is strictly greater than its neighbors. Given a 0-indexed integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to any of the peaks. You must write an algorithm that runs in $O(\log N)$ time.

## Intuition & Approach
Binary Search Gradient Climbing:
1. For midpoint `mid`: compare `nums[mid]` with its right neighbor `nums[mid + 1]`.
2. If `nums[mid] < nums[mid + 1]`, the slope is rising to the right. Since array boundaries drop to $-\infty$, a peak is guaranteed to exist on the right: `low = mid + 1`.
3. If `nums[mid] > nums[mid + 1]`, the slope is falling to the right. A peak is guaranteed to exist at `mid` or to the left: `high = mid`.
4. Converges to a peak in $O(\log N)$ time.
5. Time Complexity: $O(\log N)$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function findPeakElement(nums: number[]): number {
  let low = 0;
  let high = nums.length - 1;

  while (low < high) {
    const mid = low + Math.floor((high - low) / 2);
    if (nums[mid] < nums[mid + 1]) {
      low = mid + 1;
    } else {
      high = mid;
    }
  }

  return low;
}
```
