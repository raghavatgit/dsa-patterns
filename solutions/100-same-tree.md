# 100. Same Tree

## Complexity
- Time Complexity: O(min(n, m))
- Space Complexity: O(min(h1, h2))

## Rust Implementation
```rust
pub fn is_same_tree(p: Option<Rc<RefCell<TreeNode>>>, q: Option<Rc<RefCell<TreeNode>>>) -> bool {
    match (p, q) {
        (None, None) => true,
        (Some(p_node), Some(q_node)) => {
            let p_b = p_node.borrow();
            let q_b = q_node.borrow();
            p_b.val == q_b.val
                && is_same_tree(p_b.left.clone(), q_b.left.clone())
                && is_same_tree(p_b.right.clone(), q_b.right.clone())
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
    return p.val === q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```
