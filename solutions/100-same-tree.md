# 100. Same Tree

## Complexity
- Time Complexity: O(min(n, m))
- Space Complexity: O(min(h1, h2))

## Rust Implementation
```rust
pub fn is_same_tree(p: Option<Rc<RefCell<TreeNode>>>, q: Option<Rc<RefCell<TreeNode>>>) -> bool {
    match (p, q) {
        (None, None) => true,
        (Some(n1), Some(n2)) => {
            let b1 = n1.borrow();
            let b2 = n2.borrow();
            b1.val == b2.val
                && is_same_tree(b1.left.clone(), b2.left.clone())
                && is_same_tree(b1.right.clone(), b2.right.clone())
        }
        _ => false,
    }
}
```

## TypeScript Implementation
```typescript
export function isSameTree(p: TreeNode | null, q: TreeNode | null): boolean {
    if (!p && !q) return true;
    if (!p || !q) return false;
    if (p.val !== q.val) return false;
    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```
