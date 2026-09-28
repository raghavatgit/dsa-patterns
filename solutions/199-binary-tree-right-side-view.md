# 199. Binary Tree Right Side View

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(w)

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn right_side_view(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<i32> {
    let mut res = Vec::new();
    let root = match root {
        Some(r) => r,
        None => return res,
    };

    let mut queue = VecDeque::new();
    queue.push_back(root);

    while !queue.is_empty() {
        let len = queue.len();
        for i in 0..len {
            let node = queue.pop_front().unwrap();
            let b = node.borrow();
            if i == len - 1 {
                res.push(b.val);
            }
            if let Some(left) = b.left.clone() { queue.push_back(left); }
            if let Some(right) = b.right.clone() { queue.push_back(right); }
        }
    }

    res
}
```

## TypeScript Implementation
```typescript
export function rightSideView(root: TreeNode | null): number[] {
    if (!root) return [];
    const res: number[] = [];
    const queue: TreeNode[] = [root];

    while (queue.length > 0) {
        const len = queue.length;
        for (let i = 0; i < len; i++) {
            const node = queue.shift()!;
            if (i === len - 1) res.push(node.val);
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
    }

    return res;
}
```
