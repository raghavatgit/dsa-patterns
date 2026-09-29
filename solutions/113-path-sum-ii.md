# 113. Path Sum II

## Complexity
- Time Complexity: O(n^2) worst case copying paths in leaf nodes
- Space Complexity: O(h) stack and path buffer

## Rust Implementation
```rust
pub fn path_sum(root: Option<Rc<RefCell<TreeNode>>>, target_sum: i32) -> Vec<Vec<i32>> {
    let mut result = Vec::new();
    let mut current_path = Vec::new();

    fn dfs(
        node_opt: &Option<Rc<RefCell<TreeNode>>>,
        rem: i32,
        path: &mut Vec<i32>,
        res: &mut Vec<Vec<i32>>
    ) {
        if let Some(node) = node_opt {
            let b = node.borrow();
            path.push(b.val);
            let next_rem = rem - b.val;
            if b.left.is_none() && b.right.is_none() && next_rem == 0 {
                res.push(path.clone());
            } else {
                dfs(&b.left, next_rem, path, res);
                dfs(&b.right, next_rem, path, res);
            }
            path.pop();
        }
    }

    dfs(&root, target_sum, &mut current_path, &mut result);
    result
}
```

## TypeScript Implementation
```typescript
export function pathSum(root: TreeNode | null, targetSum: number): number[][] {
    const result: number[][] = [];
    const path: number[] = [];

    function dfs(node: TreeNode | null, rem: number): void {
        if (!node) return;
        path.push(node.val);
        const nextRem = rem - node.val;
        if (!node.left && !node.right && nextRem === 0) {
            result.push([...path]);
        } else {
            dfs(node.left, nextRem);
            dfs(node.right, nextRem);
        }
        path.pop();
    }

    dfs(root, targetSum);
    return result;
}
```
