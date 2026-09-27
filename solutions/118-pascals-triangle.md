# 118. Pascal's Triangle

## Problem Statement
Given an integer `numRows`, return the first `numRows` of Pascal's triangle.

---

## TypeScript Implementation

```typescript
export function generate(numRows: number): number[][] {
  const triangle: number[][] = [];

  for (let r = 0; r < numRows; r++) {
    const row = new Array(r + 1).fill(1);
    for (let c = 1; c < r; c++) {
      row[c] = triangle[r - 1][c - 1] + triangle[r - 1][c];
    }
    triangle.push(row);
  }

  return triangle;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(numRows^2) total entries.
* **Space Complexity:** O(numRows^2) output triangle.
