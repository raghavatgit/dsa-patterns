# 222. Count Complete Tree Nodes

## Problem Statement
Given the `root` of a complete binary tree, return the number of nodes in the tree in less than O(N) time.

---

## Binary Search on Leaf Depths
Check left-most and right-most path heights. If equal, left subtree is a full tree of size `2^d - 1`. Recurse on remaining half.

---

## TypeScript Implementation

```typescript
export function countNodes(root: TreeNode | null): number {
  if (!root) return 0;
  const lH = getLeftHeight(root);
  const rH = getRightHeight(root);

  if (lH === rH) {
    return (1 << lH) - 1;
  }

  return 1 + countNodes(root.left) + countNodes(root.right);
}

function getLeftHeight(node: TreeNode | null): number {
  let h = 0;
  while (node) { h++; node = node.left; }
  return h;
}

function getRightHeight(node: TreeNode | null): number {
  let h = 0;
  while (node) { h++; node = node.right; }
  return h;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(log^2 N).
* **Space Complexity:** O(log N) stack.
