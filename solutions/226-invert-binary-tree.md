# Problem: Invert Binary Tree

## Problem Statement
Given the root of a binary tree, invert the tree, and return its root.

## Intuition & Approach
Recursive Post-Order Swap:
1. Base case: If root is null, return null.
2. Recursively invert left subtree: `left = invertTree(root.left)`.
3. Recursively invert right subtree: `right = invertTree(root.right)`.
4. Swap child pointers: `root.left = right`, `root.right = left`.
5. Time Complexity: $O(N)$ visiting each node once. Space Complexity: $O(H)$ recursion stack.

## TypeScript Implementation

```typescript
export class TreeNode {
  val: number;
  left: TreeNode | null;
  right: TreeNode | null;
  constructor(val: number = 0, left: TreeNode | null = null, right: TreeNode | null = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

export function invertTree(root: TreeNode | null): TreeNode | null {
  if (root === null) return null;

  const left = invertTree(root.left);
  const right = invertTree(root.right);

  root.left = right;
  root.right = left;

  return root;
}
```
