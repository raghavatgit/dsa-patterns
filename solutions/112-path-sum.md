# 112. Path Sum

## Problem Statement
Given the `root` of a binary tree and an integer `targetSum`, return `true` if the tree has a root-to-leaf path such that adding up all the values along the path equals `targetSum`.

---

## TypeScript Implementation

```typescript
export function hasPathSum(root: TreeNode | null, targetSum: number): boolean {
  if (!root) return false;
  if (!root.left && !root.right) return root.val === targetSum;

  const remaining = targetSum - root.val;
  return hasPathSum(root.left, remaining) || hasPathSum(root.right, remaining);
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) visits each node once.
* **Space Complexity:** O(H) recursion stack.
