# Problem: Sqrt(x)

## Problem Statement
Given a non-negative integer `x`, return the square root of `x` rounded down to the nearest integer. The returned integer should be non-negative as well. You must not use any built-in exponent function or operator.

## Intuition & Approach
Monotonic Integer Binary Search:
1. Search range: $[0, x]$.
2. Avoid multiplication overflow: compare `mid <= x / mid` instead of `mid * mid <= x`.
3. If `mid <= x / mid`, `mid` is a valid candidate: record `ans = mid`, search higher `low = mid + 1`.
4. Otherwise, `mid` is too large: `high = mid - 1`.
5. Time Complexity: $O(\log X)$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function mySqrt(x: number): number {
  if (x < 2) return x;

  let low = 1;
  let high = Math.floor(x / 2);
  let ans = 1;

  while (low <= high) {
    const mid = low + Math.floor((high - low) / 2);
    if (mid <= Math.floor(x / mid)) {
      ans = mid;
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return ans;
}
```
