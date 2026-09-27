# 338. Counting Bits

## Problem Statement
Given an integer `n`, return an array `ans` of length `n + 1` such that for each `i` (`0 <= i <= n`), `ans[i]` is the number of `1`'s in the binary representation of `i`.

---

## Dynamic Programming Invariant
`ans[i] = ans[i >> 1] + (i & 1)`. The number of set bits in `i` equals the number of set bits in `i / 2` plus the least significant bit.

---

## TypeScript Implementation

```typescript
export function countBits(n: number): number[] {
  const ans = new Array(n + 1).fill(0);
  for (let i = 1; i <= n; i++) {
    ans[i] = ans[i >> 1] + (i & 1);
  }
  return ans;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) single pass.
* **Space Complexity:** O(N) output buffer.
