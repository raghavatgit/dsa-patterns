# 112. Path Sum

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn has_path_sum(root: Option<Rc<RefCell<TreeNode>>>, target_sum: i32) -> bool {
    match root {
        None => false,
        Some(node) => {
            let b = node.borrow();
            let remaining = target_sum - b.val;
            if b.left.is_none() && b.right.is_none() {
                return remaining == 0;
            }
            has_path_sum(b.left.clone(), remaining) || has_path_sum(b.right.clone(), remaining)
        }
    }
}
```

## TypeScript Implementation
```typescript
export function hasPathSum(root: TreeNode | null, targetSum: number): boolean {
    if (!root) return false;
    const rem = targetSum - root.val;
    if (!root.left && !root.right) return rem === 0;
    return hasPathSum(root.left, rem) || hasPathSum(root.right, rem);
}
```
