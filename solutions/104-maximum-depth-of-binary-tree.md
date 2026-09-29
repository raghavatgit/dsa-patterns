# 104. Maximum Depth of Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h) recursion stack

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn max_depth(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    match root {
        None => 0,
        Some(node) => {
            let n = node.borrow();
            1 + max_depth(n.left.clone()).max(max_depth(n.right.clone()))
        }
    }
}
```
