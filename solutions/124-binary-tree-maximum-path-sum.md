# 124. Binary Tree Maximum Path Sum

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn max_path_sum(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    let mut global_max = i32::MIN;

    fn max_gain(node: &Option<Rc<RefCell<TreeNode>>>, global_max: &mut i32) -> i32 {
        match node {
            None => 0,
            Some(n) => {
                let b = n.borrow();
                let left_gain = max_gain(&b.left, global_max).max(0);
                let right_gain = max_gain(&b.right, global_max).max(0);
                let current_path = b.val + left_gain + right_gain;
                *global_max = (*global_max).max(current_path);
                b.val + left_gain.max(right_gain)
            }
        }
    }

    max_gain(&root, &mut global_max);
    global_max
}
```

## TypeScript Implementation
```typescript
export function maxPathSum(root: TreeNode | null): number {
    let globalMax = -Infinity;

    function maxGain(node: TreeNode | null): number {
        if (!node) return 0;
        const leftGain = Math.max(0, maxGain(node.left));
        const rightGain = Math.max(0, maxGain(node.right));
        const pathSum = node.val + leftGain + rightGain;
        globalMax = Math.max(globalMax, pathSum);
        return node.val + Math.max(leftGain, rightGain);
    }

    maxGain(root);
    return globalMax;
}
```
