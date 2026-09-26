# 110. Balanced Binary Tree

## Problem Statement
Given a binary tree, determine if it is height-balanced (depth of the two subtrees of every node never differs by more than 1).

---

## Bottom-Up Early Exit
Compute subtree heights recursively. If any subtree is unbalanced, return `-1` to propagate failure without redundant checks.

---

## TypeScript Implementation

```typescript
export function isBalanced(root: TreeNode | null): boolean {
  function checkHeight(node: TreeNode | null): number {
    if (!node) return 0;

    const left = checkHeight(node.left);
    if (left === -1) return -1;

    const right = checkHeight(node.right);
    if (right === -1) return -1;

    if (Math.abs(left - right) > 1) return -1;
    return Math.max(left, right) + 1;
  }

  return checkHeight(root) !== -1;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) single bottom-up traversal.
* **Space Complexity:** O(H) recursion stack.
