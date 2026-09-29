# 230. Kth Smallest Element in a BST

## Complexity
- Time Complexity: O(h + k)
- Space Complexity: O(h)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn kth_smallest(root: Option<Rc<RefCell<TreeNode>>>, mut k: i32) -> i32 {
    let mut stack = Vec::new();
    let mut curr = root;

    while curr.is_some() || !stack.is_empty() {
        while let Some(node) = curr {
            curr = node.borrow().left.clone();
            stack.push(node);
        }
        let node = stack.pop().unwrap();
        k -= 1;
        if k == 0 { return node.borrow().val; }
        curr = node.borrow().right.clone();
    }
    -1
}
```
