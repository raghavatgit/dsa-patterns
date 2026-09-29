# 102. Binary Tree Level Order Traversal

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;

pub fn level_order(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<Vec<i32>> {
    let mut res = Vec::new();
    let mut q = VecDeque::new();
    if let Some(r) = root { q.push_back(r); }

    while !q.is_empty() {
        let size = q.len();
        let mut level = Vec::with_capacity(size);
        for _ in 0..size {
            let node = q.pop_front().unwrap();
            let n = node.borrow();
            level.push(n.val);
            if let Some(left) = n.left.clone() { q.push_back(left); }
            if let Some(right) = n.right.clone() { q.push_back(right); }
        }
        res.push(level);
    }
    res
}
```
