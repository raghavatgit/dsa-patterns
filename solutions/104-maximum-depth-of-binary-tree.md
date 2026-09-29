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
            let left = max_depth(node.borrow().left.clone());
            let right = max_depth(node.borrow().right.clone());
            1 + left.max(right)
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
