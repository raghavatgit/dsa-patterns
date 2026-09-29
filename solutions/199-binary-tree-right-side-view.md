# 199. Binary Tree Right Side View

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;

pub fn right_side_view(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<i32> {
    let mut res = Vec::new();
    let mut q = VecDeque::new();
    if let Some(r) = root { q.push_back(r); }

    while !q.is_empty() {
        let size = q.len();
        for i in 0..size {
            let node = q.pop_front().unwrap();
            let n = node.borrow();
            if i == size - 1 { res.push(n.val); }
            if let Some(left) = n.left.clone() { q.push_back(left); }
            if let Some(right) = n.right.clone() { q.push_back(right); }
        }
    }
    res
}
```
