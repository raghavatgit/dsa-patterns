# 543. Diameter of Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn diameter_of_binary_tree(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    let mut diameter = 0;

    fn depth(node: Option<Rc<RefCell<TreeNode>>>, diameter: &mut i32) -> i32 {
        let node = match node {
            Some(n) => n,
            None => return 0,
        };
        let b = node.borrow();
        let left = depth(b.left.clone(), diameter);
        let right = depth(b.right.clone(), diameter);

        *diameter = std::cmp::max(*diameter, left + right);
        1 + std::cmp::max(left, right)
    }

    depth(root, &mut diameter);
    diameter
}
```

## TypeScript Implementation
```typescript
export function diameterOfBinaryTree(root: TreeNode | null): number {
    let diameter = 0;
    const depth = (node: TreeNode | null): number => {
        if (!node) return 0;
        const left = depth(node.left);
        const right = depth(node.right);
        diameter = Math.max(diameter, left + right);
        return 1 + Math.max(left, right);
    };
    depth(root);
    return diameter;
}
```
