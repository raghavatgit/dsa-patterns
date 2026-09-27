# 144. Binary Tree Preorder Traversal

## Problem Statement
Given the `root` of a binary tree, return the preorder traversal of its nodes' values iteratively.

---

## TypeScript Implementation

```typescript
export function preorderTraversal(root: TreeNode | null): number[] {
  if (!root) return [];
  const result: number[] = [];
  const stack: TreeNode[] = [root];

  while (stack.length > 0) {
    const node = stack.pop()!;
    result.push(node.val);
    if (node.right) stack.push(node.right);
    if (node.left) stack.push(node.left);
  }

  return result;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) visits every node.
* **Space Complexity:** O(H) stack depth.
