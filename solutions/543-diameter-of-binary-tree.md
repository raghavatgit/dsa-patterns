# Problem: Diameter of Binary Tree

## Problem Statement
Given the root of a binary tree, return the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

## Intuition & Approach
Post-Order Depth DFS with Global Maxima Tracking:
1. At each node, longest path turning at this node has length `depth(left) + depth(right)`.
2. Update global `max_diameter = max(max_diameter, depth(left) + depth(right))`.
3. Return `1 + max(depth(left), depth(right))` to caller.
4. Time Complexity: $O(N)$ single pass. Space Complexity: $O(H)$ recursion depth.

## TypeScript Implementation

```typescript
export function diameterOfBinaryTree(root: TreeNode | null): number {
  let diameter = 0;

  function depth(node: TreeNode | null): number {
    if (node === null) return 0;

    const leftDepth = depth(node.left);
    const rightDepth = depth(node.right);

    diameter = Math.max(diameter, leftDepth + rightDepth);
    return 1 + Math.max(leftDepth, rightDepth);
  }

  depth(root);
  return diameter;
}
```
