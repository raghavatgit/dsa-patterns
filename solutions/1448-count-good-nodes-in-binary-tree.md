# 1448. Count Good Nodes in Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn good_nodes(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    fn dfs(node: Option<Rc<RefCell<TreeNode>>>, mut max_val: i32) -> i32 {
        match node {
            None => 0,
            Some(n) => {
                let b = n.borrow();
                let mut count = 0;
                if b.val >= max_val {
                    count += 1;
                    max_val = b.val;
                }
                count + dfs(b.left.clone(), max_val) + dfs(b.right.clone(), max_val)
            }
        }
    }
    dfs(root, i32::MIN)
}
```
