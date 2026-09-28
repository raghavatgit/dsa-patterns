# 297. Serialize and Deserialize Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## TypeScript Implementation
```typescript
export function serialize(root: TreeNode | null): string {
    const tokens: string[] = [];
    const build = (node: TreeNode | null) => {
        if (!node) {
            tokens.push("#");
            return;
        }
        tokens.push(node.val.toString());
        build(node.left);
        build(node.right);
    };
    build(root);
    return tokens.join(",");
}

export function deserialize(data: string): TreeNode | null {
    const tokens = data.split(",");
    let index = 0;

    const build = (): TreeNode | null => {
        if (index >= tokens.length || tokens[index] === "#") {
            index++;
            return null;
        }
        const node = new TreeNode(parseInt(tokens[index++], 10));
        node.left = build();
        node.right = build();
        return node;
    };

    return build();
}
```
