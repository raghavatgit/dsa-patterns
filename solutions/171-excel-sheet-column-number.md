# 171. Excel Sheet Column Number

## Problem Statement
Given a string `columnTitle` that represents the column title as it appears in an Excel sheet, return its corresponding column number.

---

## TypeScript Implementation

```typescript
export function titleToNumber(columnTitle: string): number {
  let ans = 0;
  for (let i = 0; i < columnTitle.length; i++) {
    const d = columnTitle.charCodeAt(i) - 64;
    ans = ans * 26 + d;
  }
  return ans;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) where N is title length.
* **Space Complexity:** O(1).
