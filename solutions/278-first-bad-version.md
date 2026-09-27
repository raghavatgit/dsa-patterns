# 278. First Bad Version

## Problem Statement
You are a product manager and currently leading a team to develop a new product. Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one which causes all following to be bad.

---

## TypeScript Implementation

```typescript
export function solution(isBadVersion: (version: number) => boolean) {
  return function(n: number): number {
    let left = 1;
    let right = n;

    while (left < right) {
      const mid = left + Math.floor((right - left) / 2);
      if (isBadVersion(mid)) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }

    return left;
  };
}
```

---

## Complexity Analysis
* **Time Complexity:** O(log N).
* **Space Complexity:** O(1).
