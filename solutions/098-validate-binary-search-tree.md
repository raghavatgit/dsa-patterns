# Problem: Validate Binary Search Tree

## Problem Statement
Given the `root` of a binary tree, determine if it is a valid binary search tree (BST).
A valid BST is defined as:
* The left subtree of a node contains only nodes with keys strictly less than the node's key.
* The right subtree of a node contains only nodes with keys strictly greater than the node's key.
* Both the left and right subtrees must also be binary search trees.

## Intuition & Approach
Validating only parent-child relationships (`left < root < right`) is insufficient; all descendants in a subtree must satisfy the ancestor's range.
Pass dynamic lower and upper bounds down the recursive stack: `validate(node, min, max)`.
* For left child: upper bound becomes `node.val`.
* For right child: lower bound becomes `node.val`.

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

export function isValidBST(root: TreeNode | null): boolean {
  function validate(node: TreeNode | null, min: number | null, max: number | null): boolean {
    if (!node) return true;

    if (min !== null && node.val <= min) return false;
    if (max !== null && node.val >= max) return false;

    return (
      validate(node.left, min, node.val) &&
      validate(node.right, node.val, max)
    );
  }

  return validate(root, null, null);
}
```

## Complexity Analysis
* **Time Complexity:** O(N) visits each node once.
* **Space Complexity:** O(H) recursion stack where H is tree height.
