# 98. Validate Binary Search Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn is_valid_bst(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
    fn validate(node: Option<Rc<RefCell<TreeNode>>>, min: Option<i64>, max: Option<i64>) -> bool {
        match node {
            None => true,
            Some(n) => {
                let b = n.borrow();
                let v = b.val as i64;
                if let Some(low) = min { if v <= low { return false; } }
                if let Some(high) = max { if v >= high { return false; } }
                validate(b.left.clone(), min, Some(v)) && validate(b.right.clone(), Some(v), max)
            }
        }
    }
    validate(root, None, None)
}
```
