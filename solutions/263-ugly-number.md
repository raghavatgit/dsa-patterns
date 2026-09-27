# 263. Ugly Number

## Problem Statement
An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5. Given an integer `n`, return `true` if `n` is an ugly number.

---

## TypeScript Implementation

```typescript
export function isUgly(n: number): boolean {
  if (n <= 0) return false;
  const primes = [2, 3, 5];

  for (const p of primes) {
    while (n % p === 0) {
      n /= p;
    }
  }

  return n === 1;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(log N).
* **Space Complexity:** O(1).
