# 258. Add Digits

## Problem Statement
Given an integer `num`, repeatedly add all its digits until the result has only one digit, and return it in O(1) time.

---

## Digital Root Formula (Modulo 9)
In base 10, any number `n` is congruent to the sum of its digits modulo 9:
* If `num == 0` -> `0`
* If `num % 9 == 0` -> `9`
* Otherwise -> `num % 9`

---

## TypeScript Implementation

```typescript
export function addDigits(num: number): number {
  if (num === 0) return 0;
  return num % 9 === 0 ? 9 : num % 9;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(1).
* **Space Complexity:** O(1).
