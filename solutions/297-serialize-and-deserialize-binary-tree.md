# Problem: Serialize and Deserialize Binary Tree

## Problem Statement
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment. Design an algorithm to serialize and deserialize a binary tree.

## Intuition & Approach
Pre-order Depth First Search with Sentinel Null Tokens:
1. **Serialization**:
   - Traverse the tree in pre-order (`Root -> Left -> Right`).
   - If the current node is null, append sentinel token `"#"`.
   - Otherwise, append `node.val` followed by delimiter `","`.
2. **Deserialization**:
   - Split serialized string by delimiter into a queue of tokens.
   - Recursively construct nodes:
     - Pop token. If token is `"#"`, return null.
     - Create new `TreeNode(Number(token))`.
     - Recursively build left child, then right child.
3. Time Complexity: $O(N)$ for both serialization and deserialization. Space Complexity: $O(N)$ recursion depth and token buffer.

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

export function serialize(root: TreeNode | null): string {
  const tokens: string[] = [];

  function dfs(node: TreeNode | null) {
    if (node === null) {
      tokens.push("#");
      return;
    }
    tokens.push(String(node.val));
    dfs(node.left);
    dfs(node.right);
  }

  dfs(root);
  return tokens.join(",");
}

export function deserialize(data: string): TreeNode | null {
  const tokens = data.split(",");
  let idx = 0;

  function build(): TreeNode | null {
    if (idx >= tokens.length) return null;
    const valStr = tokens[idx++];
    if (valStr === "#") return null;

    const node = new TreeNode(Number(valStr));
    node.left = build();
    node.right = build();
    return node;
  }

  return build();
}
```
