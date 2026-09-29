# 572. Subtree of Another Tree

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(h)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn is_subtree(root: Option<Rc<RefCell<TreeNode>>>, sub_root: Option<Rc<RefCell<TreeNode>>>) -> bool {
    fn is_same(p: &Option<Rc<RefCell<TreeNode>>>, q: &Option<Rc<RefCell<TreeNode>>>) -> bool {
        match (p, q) {
            (None, None) => true,
            (Some(n1), Some(n2)) => {
                let b1 = n1.borrow();
                let b2 = n2.borrow();
                b1.val == b2.val && is_same(&b1.left, &b2.left) && is_same(&b1.right, &b2.right)
            }
            _ => false,
        }
    }

    if root.is_none() { return false; }
    if is_same(&root, &sub_root) { return true; }
    let n = root.unwrap();
    let b = n.borrow();
    is_subtree(b.left.clone(), sub_root.clone()) || is_subtree(b.right.clone(), sub_root)
}
```
