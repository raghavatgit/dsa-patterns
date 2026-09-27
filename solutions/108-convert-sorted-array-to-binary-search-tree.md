# 108. Convert Sorted Array to Binary Search Tree

## Problem Statement
Given an integer array `nums` where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.

---

## TypeScript Implementation

```typescript
export function sortedArrayToBST(nums: number[]): TreeNode | null {
  function build(left: number, right: number): TreeNode | null {
    if (left > right) return null;
    const mid = left + Math.floor((right - left) / 2);
    const root = new TreeNode(nums[mid]);
    root.left = build(left, mid - 1);
    root.right = build(mid + 1, right);
    return root;
  }

  return build(0, nums.length - 1);
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) visits each number once.
* **Space Complexity:** O(log N) recursion depth.
