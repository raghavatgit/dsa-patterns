# Problem: Lowest Common Ancestor of a Binary Tree

## Problem Statement
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes `p` and `q`. The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow a node to be a descendant of itself).

## Intuition & Approach
Post-Order DFS Tree Recursion:
1. Base cases:
   - If current node is null, return null.
   - If current node is equal to either `p` or `q`, return current node.
2. Recursively search left child: `left = lca(node.left, p, q)`.
3. Recursively search right child: `right = lca(node.right, p, q)`.
4. If both `left` and `right` are non-null, `p` and `q` are split across subtrees of current node: current node is their LCA.
5. If only one is non-null, return the non-null child.
6. Time Complexity: $O(N)$ visiting every node once. Space Complexity: $O(H)$ recursion stack depth.

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

export function lowestCommonAncestor(root: TreeNode | null, p: TreeNode | null, q: TreeNode | null): TreeNode | null {
  if (root === null || root === p || root === q) {
    return root;
  }

  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);

  if (left !== null && right !== null) {
    return root;
  }

  return left !== null ? left : right;
}
```
