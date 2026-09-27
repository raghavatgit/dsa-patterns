# 231. Power of Two

## Problem Statement
Given an integer `n`, return `true` if it is a power of two.

---

## Bitwise Property
A power of two in binary has exactly one bit set. Therefore `n > 0 && (n & (n - 1)) === 0`.

---

## TypeScript Implementation

```typescript
export function isPowerOfTwo(n: number): boolean {
  return n > 0 && (n & (n - 1)) === 0;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(1).
* **Space Complexity:** O(1).
