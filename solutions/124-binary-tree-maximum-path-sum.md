# 124. Binary Tree Maximum Path Sum

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn max_path_sum(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    let mut max_sum = i32::MIN;

    fn dfs(node: Option<Rc<RefCell<TreeNode>>>, max_sum: &mut i32) -> i32 {
        match node {
            None => 0,
            Some(n) => {
                let b = n.borrow();
                let left_gain = dfs(b.left.clone(), max_sum).max(0);
                let right_gain = dfs(b.right.clone(), max_sum).max(0);
                *max_sum = (*max_sum).max(b.val + left_gain + right_gain);
                b.val + left_gain.max(right_gain)
            }
        }
    }

    dfs(root, &mut max_sum);
    max_sum
}
```
