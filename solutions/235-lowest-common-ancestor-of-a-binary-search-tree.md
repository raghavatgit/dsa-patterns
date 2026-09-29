# 235. Lowest Common Ancestor of a BST

## Complexity
- Time Complexity: O(h)
- Space Complexity: O(1) iterative traversal

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn lowest_common_ancestor(
    mut root: Option<Rc<RefCell<TreeNode>>>,
    p: Option<Rc<RefCell<TreeNode>>>,
    q: Option<Rc<RefCell<TreeNode>>>,
) -> Option<Rc<RefCell<TreeNode>>> {
    let p_val = p.unwrap().borrow().val;
    let q_val = q.unwrap().borrow().val;

    while let Some(node) = root.clone() {
        let val = node.borrow().val;
        if p_val < val && q_val < val {
            root = node.borrow().left.clone();
        } else if p_val > val && q_val > val {
            root = node.borrow().right.clone();
        } else {
            return Some(node);
        }
    }
    None
}
```
