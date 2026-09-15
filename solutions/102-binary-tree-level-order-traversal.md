# Problem: Binary Tree Level Order Traversal

## Problem Statement
Given the `root` of a binary tree, return the level order traversal of its nodes' values (i.e., from left to right, level by level).

## Intuition & Approach
Use Breadth-First Search (BFS) with a FIFO queue. At the beginning of each outer loop iteration, capture `level_size = queue.length`. Dequeue exactly `level_size` nodes to guarantee that all nodes belonging to the current level are grouped into the same sub-array before moving to the next depth.

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

export function levelOrder(root: TreeNode | null): number[][] {
  if (!root) return [];

  const result: number[][] = [];
  const queue: TreeNode[] = [root];

  while (queue.length > 0) {
    const levelSize = queue.length;
    const currentLevel: number[] = [];

    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift()!;
      currentLevel.push(node.val);

      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }

    result.push(currentLevel);
  }

  return result;
}
```

## Complexity Analysis
* **Time Complexity:** O(N) visits each tree node once.
* **Space Complexity:** O(W) where W is maximum level width (up to N/2 in complete binary trees).
