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
            let rem = target_sum - b.val;
            if b.left.is_none() && b.right.is_none() {
                return rem == 0;
            }
            has_path_sum(b.left.clone(), rem) || has_path_sum(b.right.clone(), rem)
        }
    }
}
```

## TypeScript Implementation
```typescript
export function hasPathSum(root: TreeNode | null, targetSum: number): boolean {
    if (!root) return false;
    const remaining = targetSum - root.val;
    if (!root.left && !root.right) return remaining === 0;
    return hasPathSum(root.left, remaining) || hasPathSum(root.right, remaining);
}
```
