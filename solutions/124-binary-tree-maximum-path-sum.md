# 124. Binary Tree Maximum Path Sum

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn max_path_sum(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    let mut max_sum = i32::MIN;

    fn dfs(node: Option<Rc<RefCell<TreeNode>>>, max_sum: &mut i32) -> i32 {
        let node = match node {
            Some(n) => n,
            None => return 0,
        };
        let b = node.borrow();
        let left_gain = std::cmp::max(0, dfs(b.left.clone(), max_sum));
        let right_gain = std::cmp::max(0, dfs(b.right.clone(), max_sum));

        let current_path = b.val + left_gain + right_gain;
        *max_sum = std::cmp::max(*max_sum, current_path);

        b.val + std::cmp::max(left_gain, right_gain)
    }

    dfs(root, &mut max_sum);
    max_sum
}
```

## TypeScript Implementation
```typescript
export function maxPathSum(root: TreeNode | null): number {
    let maxSum = -Infinity;

    const dfs = (node: TreeNode | null): number => {
        if (!node) return 0;
        const leftGain = Math.max(0, dfs(node.left));
        const rightGain = Math.max(0, dfs(node.right));
        const currentPath = node.val + leftGain + rightGain;
        maxSum = Math.max(maxSum, currentPath);
        return node.val + Math.max(leftGain, rightGain);
    };

    dfs(root);
    return maxSum;
}
```
