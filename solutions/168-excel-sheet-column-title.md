# 168. Excel Sheet Column Title

## Problem Statement
Given an integer `columnNumber`, return its corresponding column title as it appears in an Excel sheet (e.g. 1 -> A, 28 -> AB).

---

## TypeScript Implementation

```typescript
export function convertToTitle(columnNumber: number): string {
  const result: string[] = [];

  while (columnNumber > 0) {
    columnNumber--; // Offset to 0-indexed base-26
    const rem = columnNumber % 26;
    result.push(String.fromCharCode(65 + rem));
    columnNumber = Math.floor(columnNumber / 26);
  }

  return result.reverse().join('');
}
```

---

## Complexity Analysis
* **Time Complexity:** O(log26 N).
* **Space Complexity:** O(1) auxiliary space.
