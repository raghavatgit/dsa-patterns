# 257. Binary Tree Paths

## Problem Statement
Given the `root` of a binary tree, return all root-to-leaf paths in any order.

---

## TypeScript Implementation

```typescript
export function binaryTreePaths(root: TreeNode | null): string[] {
  const paths: string[] = [];
  if (!root) return paths;

  function dfs(node: TreeNode, currentPath: string) {
    if (!node.left && !node.right) {
      paths.push(currentPath + node.val);
      return;
    }
    if (node.left) dfs(node.left, currentPath + node.val + "->");
    if (node.right) dfs(node.right, currentPath + node.val + "->");
  }

  dfs(root, "");
  return paths;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) visits each node.
* **Space Complexity:** O(H) recursion depth.
