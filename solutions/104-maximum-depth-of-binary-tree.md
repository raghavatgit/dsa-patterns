# Problem: Maximum Depth of Binary Tree

## Problem Statement
Given the root of a binary tree, return its maximum depth. A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

## Intuition & Approach
1. Base case: If `root === null`, depth is 0.
2. Recursively calculate depth of subtrees: `1 + max(maxDepth(root.left), maxDepth(root.right))`.
3. Time Complexity: $O(N)$. Space Complexity: $O(H)$ stack depth.

## TypeScript Implementation

```typescript
export function maxDepth(root: TreeNode | null): number {
  if (root === null) return 0;
  return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```
