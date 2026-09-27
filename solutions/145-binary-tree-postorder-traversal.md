# 145. Binary Tree Postorder Traversal

## Problem Statement
Given the `root` of a binary tree, return the postorder traversal of its nodes' values iteratively.

---

## TypeScript Implementation

```typescript
export function postorderTraversal(root: TreeNode | null): number[] {
  if (!root) return [];
  const s1: TreeNode[] = [root];
  const s2: TreeNode[] = [];

  while (s1.length > 0) {
    const node = s1.pop()!;
    s2.push(node);
    if (node.left) s1.push(node.left);
    if (node.right) s1.push(node.right);
  }

  const result: number[] = [];
  while (s2.length > 0) {
    result.push(s2.pop()!.val);
  }
  return result;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N).
* **Space Complexity:** O(N).
