# 104. Maximum Depth of Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn max_depth(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    match root {
        None => 0,
        Some(node) => {
            let b = node.borrow();
            1 + std::cmp::max(max_depth(b.left.clone()), max_depth(b.right.clone()))
        }
    }
}
```

## TypeScript Implementation
```typescript
export function maxDepth(root: TreeNode | null): number {
    if (!root) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```
