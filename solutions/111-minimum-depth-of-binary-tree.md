# 111. Minimum Depth of Binary Tree

## Problem Statement
Given a binary tree, find its minimum depth (the number of nodes along the shortest path from root down to nearest leaf).

---

## TypeScript Implementation

```typescript
export function minDepth(root: TreeNode | null): number {
  if (!root) return 0;
  const queue: [TreeNode, number][] = [[root, 1]];

  while (queue.length > 0) {
    const [node, depth] = queue.shift()!;
    if (!node.left && !node.right) return depth;
    if (node.left) queue.push([node.left, depth + 1]);
    if (node.right) queue.push([node.right, depth + 1]);
  }

  return 0;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) visits nodes level by level.
* **Space Complexity:** O(W) where W is maximum tree width.
