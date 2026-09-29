# 100. Same Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn is_same_tree(p: Option<Rc<RefCell<TreeNode>>>, q: Option<Rc<RefCell<TreeNode>>>) -> bool {
    match (p, q) {
        (None, None) => true,
        (Some(n1), Some(n2)) => {
            let b1 = n1.borrow();
            let b2 = n2.borrow();
            b1.val == b2.val && is_same_tree(b1.left.clone(), b2.left.clone()) && is_same_tree(b1.right.clone(), b2.right.clone())
        }
        _ => false,
    }
}
```
