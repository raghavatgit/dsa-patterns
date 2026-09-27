# 228. Summary Ranges

## Problem Statement
Given a sorted unique integer array `nums`, return the smallest sorted list of ranges that cover all the numbers in the array exactly.

---

## TypeScript Implementation

```typescript
export function summaryRanges(nums: number[]): string[] {
  const result: string[] = [];
  let i = 0;

  while (i < nums.length) {
    const start = nums[i];
    while (i + 1 < nums.length && nums[i + 1] === nums[i] + 1) {
      i++;
    }
    const end = nums[i];
    if (start === end) {
      result.push(`${start}`);
    } else {
      result.push(`${start}->${end}`);
    }
    i++;
  }

  return result;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N).
* **Space Complexity:** O(1) extra space.
