# 202. Happy Number

## Problem Statement
Determine if a number `n` is happy (iteratively replacing by sum of squares of digits reaches 1).

---

## TypeScript Implementation

```typescript
export function isHappy(n: number): boolean {
  function getNext(num: number): number {
    let total = 0;
    while (num > 0) {
      const d = num % 10;
      total += d * d;
      num = Math.floor(num / 10);
    }
    return total;
  }

  let slow = n;
  let fast = getNext(n);

  while (fast !== 1 && slow !== fast) {
    slow = getNext(slow);
    fast = getNext(getNext(fast));
  }

  return fast === 1;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(log N).
* **Space Complexity:** O(1) Floyd cycle pointer.
