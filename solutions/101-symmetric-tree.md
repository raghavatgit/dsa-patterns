# 101. Symmetric Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn is_symmetric(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
    fn is_mirror(t1: Option<Rc<RefCell<TreeNode>>>, t2: Option<Rc<RefCell<TreeNode>>>) -> bool {
        match (t1, t2) {
            (None, None) => true,
            (Some(n1), Some(n2)) => {
                let b1 = n1.borrow();
                let b2 = n2.borrow();
                b1.val == b2.val
                    && is_mirror(b1.left.clone(), b2.right.clone())
                    && is_mirror(b1.right.clone(), b2.left.clone())
            }
            _ => false,
        }
    }

    match root {
        None => true,
        Some(node) => is_mirror(node.borrow().left.clone(), node.borrow().right.clone()),
    }
}
```

## TypeScript Implementation
```typescript
export function isSymmetric(root: TreeNode | null): boolean {
    if (!root) return true;
    const isMirror = (t1: TreeNode | null, t2: TreeNode | null): boolean => {
        if (!t1 && !t2) return true;
        if (!t1 || !t2) return false;
        return t1.val === t2.val && isMirror(t1.left, t2.right) && isMirror(t1.right, t2.left);
    };
    return isMirror(root.left, root.right);
}
```
