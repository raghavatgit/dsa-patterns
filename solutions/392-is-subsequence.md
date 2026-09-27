# 392. Is Subsequence

## Problem Statement
Given two strings `s` and `t`, return `true` if `s` is a subsequence of `t`, or `false` otherwise.

---

## TypeScript Implementation

```typescript
export function isSubsequence(s: string, t: string): boolean {
  let pS = 0;
  let pT = 0;

  while (pS < s.length && pT < t.length) {
    if (s[pS] === t[pT]) {
      pS++;
    }
    pT++;
  }

  return pS === s.length;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) where N is length of t.
* **Space Complexity:** O(1).
