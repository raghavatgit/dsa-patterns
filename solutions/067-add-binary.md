# 067. Add Binary

## Problem Statement
Given two binary strings `a` and `b`, return their sum as a binary string.

---

## TypeScript Implementation

```typescript
export function addBinary(a: string, b: string): string {
  let i = a.length - 1;
  let j = b.length - 1;
  let carry = 0;
  const result: string[] = [];

  while (i >= 0 || j >= 0 || carry > 0) {
    let sum = carry;
    if (i >= 0) sum += a.charCodeAt(i--) - 48;
    if (j >= 0) sum += b.charCodeAt(j--) - 48;

    result.push(String(sum % 2));
    carry = Math.floor(sum / 2);
  }

  return result.reverse().join('');
}
```

---

## Complexity Analysis
* **Time Complexity:** O(max(N, M)).
* **Space Complexity:** O(max(N, M)).
