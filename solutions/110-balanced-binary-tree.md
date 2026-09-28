# 110. Balanced Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn is_balanced(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
    fn check_height(node: Option<Rc<RefCell<TreeNode>>>) -> i32 {
        let node = match node {
            Some(n) => n,
            None => return 0,
        };
        let b = node.borrow();
        let left = check_height(b.left.clone());
        if left == -1 { return -1; }
        let right = check_height(b.right.clone());
        if right == -1 { return -1; }

        if (left - right).abs() > 1 {
            -1
        } else {
            1 + std::cmp::max(left, right)
        }
    }

    check_height(root) != -1
}
```

## TypeScript Implementation
```typescript
export function isBalanced(root: TreeNode | null): boolean {
    const checkHeight = (node: TreeNode | null): number => {
        if (!node) return 0;
        const left = checkHeight(node.left);
        if (left === -1) return -1;
        const right = checkHeight(node.right);
        if (right === -1) return -1;

        if (Math.abs(left - right) > 1) return -1;
        return 1 + Math.max(left, right);
    };

    return checkHeight(root) !== -1;
}
```
