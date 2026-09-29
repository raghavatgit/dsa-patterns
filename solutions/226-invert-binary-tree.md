# 226. Invert Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn invert_tree(root: Option<Rc<RefCell<TreeNode>>>) -> Option<Rc<RefCell<TreeNode>>> {
    if let Some(node) = root.clone() {
        let mut n = node.borrow_mut();
        let left = invert_tree(n.left.take());
        let right = invert_tree(n.right.take());
        n.left = right;
        n.right = left;
    }
    root
}
```
