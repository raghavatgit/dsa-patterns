# 088. Merge Sorted Array

## Problem Statement
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`. Merge `nums2` into `nums1` as one sorted array in-place.

---

## Three-Pointer Reverse Placement
Place the largest element from `nums1` and `nums2` starting from the end of `nums1` (`m + n - 1`), avoiding overwriting existing elements.

---

## TypeScript Implementation

```typescript
export function merge(nums1: number[], m: number, nums2: number[], n: number): void {
  let p1 = m - 1;
  let p2 = n - 1;
  let write = m + n - 1;

  while (p2 >= 0) {
    if (p1 >= 0 && nums1[p1] > nums2[p2]) {
      nums1[write--] = nums1[p1--];
    } else {
      nums1[write--] = nums2[p2--];
    }
  }
}
```

---

## Complexity Analysis
* **Time Complexity:** O(M + N).
* **Space Complexity:** O(1) in-place.
