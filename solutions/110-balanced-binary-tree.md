# 110. Balanced Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn is_balanced(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
    fn check_height(node: &Option<Rc<RefCell<TreeNode>>>) -> Option<i32> {
        match node {
            None => Some(0),
            Some(n) => {
                let b = n.borrow();
                let left_h = check_height(&b.left)?;
                let right_h = check_height(&b.right)?;
                if (left_h - right_h).abs() > 1 {
                    None
                } else {
                    Some(1 + left_h.max(right_h))
                }
            }
        }
    }
    check_height(&root).is_some()
}
```

## TypeScript Implementation
```typescript
export function isBalanced(root: TreeNode | null): boolean {
    function check(node: TreeNode | null): number {
        if (!node) return 0;
        const left = check(node.left);
        if (left === -1) return -1;
        const right = check(node.right);
        if (right === -1) return -1;

        if (Math.abs(left - right) > 1) return -1;
        return 1 + Math.max(left, right);
    }
    return check(root) !== -1;
}
```
