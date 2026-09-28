# 102. Binary Tree Level Order Traversal

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(w) where w is tree maximum width

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn level_order(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<Vec<i32>> {
    let mut res = Vec::new();
    let root = match root {
        Some(r) => r,
        None => return res,
    };

    let mut queue = VecDeque::new();
    queue.push_back(root);

    while !queue.is_empty() {
        let level_len = queue.len();
        let mut level_vals = Vec::with_capacity(level_len);

        for _ in 0..level_len {
            let node = queue.pop_front().unwrap();
            let b = node.borrow();
            level_vals.push(b.val);
            if let Some(left) = b.left.clone() {
                queue.push_back(left);
            }
            if let Some(right) = b.right.clone() {
                queue.push_back(right);
            }
        }
        res.push(level_vals);
    }

    res
}
```

## TypeScript Implementation
```typescript
export function levelOrder(root: TreeNode | null): number[][] {
    if (!root) return [];
    const res: number[][] = [];
    const queue: TreeNode[] = [root];

    while (queue.length > 0) {
        const len = queue.length;
        const currentLevel: number[] = [];
        for (let i = 0; i < len; i++) {
            const node = queue.shift()!;
            currentLevel.push(node.val);
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
        res.push(currentLevel);
    }

    return res;
}
```
