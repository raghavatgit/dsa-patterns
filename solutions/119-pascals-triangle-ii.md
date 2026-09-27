# 119. Pascal's Triangle II

## Problem Statement
Given an integer `rowIndex`, return the `rowIndex`-th (0-indexed) row of Pascal's triangle using only O(rowIndex) extra space.

---

## TypeScript Implementation

```typescript
export function getRow(rowIndex: number): number[] {
  const row = new Array(rowIndex + 1).fill(1);
  for (let r = 2; r <= rowIndex; r++) {
    for (let c = r - 1; c >= 1; c--) {
      row[c] += row[c - 1];
    }
  }
  return row;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(K^2).
* **Space Complexity:** O(K) optimal in-place buffer.
