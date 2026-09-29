# 102. Binary Tree Level Order Traversal

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(w) maximum level width

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn level_order(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<Vec<i32>> {
    let mut result = Vec::new();
    let root_node = match root {
        Some(r) => r,
        None => return result,
    };

    let mut queue = VecDeque::new();
    queue.push_back(root_node);

    while !queue.is_empty() {
        let level_size = queue.len();
        let mut level_nodes = Vec::with_capacity(level_size);

        for _ in 0..level_size {
            if let Some(curr) = queue.pop_front() {
                let borrowed = curr.borrow();
                level_nodes.push(borrowed.val);
                if let Some(ref left) = borrowed.left {
                    queue.push_back(Rc::clone(left));
                }
                if let Some(ref right) = borrowed.right {
                    queue.push_back(Rc::clone(right));
                }
            }
        }
        result.push(level_nodes);
    }
    result
}
```

## TypeScript Implementation
```typescript
export function levelOrder(root: TreeNode | null): number[][] {
    if (!root) return [];
    const result: number[][] = [];
    const queue: TreeNode[] = [root];

    while (queue.length > 0) {
        const levelSize = queue.length;
        const currentLevel: number[] = [];

        for (let i = 0; i < levelSize; i++) {
            const node = queue.shift()!;
            currentLevel.push(node.val);
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
        result.push(currentLevel);
    }
    return result;
}
```
