# 094. Binary Tree Inorder Traversal

## Problem Statement
Given the `root` of a binary tree, return the inorder traversal of its nodes' values using O(1) auxiliary space (Morris Traversal).

---

## Morris Threading Mechanics
Create temporary predecessor threads from the rightmost child of the left subtree pointing back to the current node. This enables traversal backtracking without a runtime call stack.

---

## TypeScript Implementation

```typescript
export function inorderTraversal(root: TreeNode | null): number[] {
  const result: number[] = [];
  let curr = root;

  while (curr !== null) {
    if (curr.left === null) {
      result.push(curr.val);
      curr = curr.right;
    } else {
      let pred = curr.left;
      while (pred.right !== null && pred.right !== curr) {
        pred = pred.right;
      }

      if (pred.right === null) {
        pred.right = curr; // Construct thread
        curr = curr.left;
      } else {
        pred.right = null; // Sever thread
        result.push(curr.val);
        curr = curr.right;
      }
    }
  }

  return result;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) each edge traversed at most three times.
* **Space Complexity:** O(1) true constant auxiliary space.
