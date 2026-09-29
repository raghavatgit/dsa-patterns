# 103. Binary Tree Zigzag Level Order Traversal

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(w)

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn zigzag_level_order(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<Vec<i32>> {
    let mut res = Vec::new();
    let root_node = match root { Some(r) => r, None => return res };
    let mut q = VecDeque::new();
    q.push_back(root_node);
    let mut left_to_right = true;

    while !q.is_empty() {
        let len = q.len();
        let mut level = VecDeque::with_capacity(len);
        for _ in 0..len {
            let node = q.pop_front().unwrap();
            let b = node.borrow();
            if left_to_right {
                level.push_back(b.val);
            } else {
                level.push_front(b.val);
            }
            if let Some(ref l) = b.left { q.push_back(Rc::clone(l)); }
            if let Some(ref r) = b.right { q.push_back(Rc::clone(r)); }
        }
        res.push(level.into_iter().collect());
        left_to_right = !left_to_right;
    }
    res
}
```

## TypeScript Implementation
```typescript
export function zigzagLevelOrder(root: TreeNode | null): number[][] {
    if (!root) return [];
    const result: number[][] = [];
    const queue: TreeNode[] = [root];
    let leftToRight = true;

    while (queue.length > 0) {
        const size = queue.length;
        const level: number[] = new Array(size);

        for (let i = 0; i < size; i++) {
            const node = queue.shift()!;
            const idx = leftToRight ? i : size - 1 - i;
            level[idx] = node.val;
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
        result.push(level);
        leftToRight = !leftToRight;
    }
    return result;
}
```
