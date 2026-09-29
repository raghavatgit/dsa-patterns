# 105. Construct Binary Tree from Preorder and Inorder Traversal

## Complexity
- Time Complexity: O(n) with in-order index hash map
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::HashMap;

pub fn build_tree(preorder: Vec<i32>, inorder: Vec<i32>) -> Option<Rc<RefCell<TreeNode>>> {
    let in_map: HashMap<i32, usize> = inorder.iter().enumerate().map(|(i, &v)| (v, i)).collect();
    let mut pre_idx = 0;

    fn helper(pre: &[i32], in_map: &HashMap<i32, usize>, pre_idx: &mut usize, in_start: usize, in_end: usize) -> Option<Rc<RefCell<TreeNode>>> {
        if in_start > in_end || in_end >= in_map.len() { return None; }
        let root_val = pre[*pre_idx];
        *pre_idx += 1;

        let root = Rc::new(RefCell::new(TreeNode::new(root_val)));
        let root_in_idx = in_map[&root_val];

        if root_in_idx > in_start {
            root.borrow_mut().left = helper(pre, in_map, pre_idx, in_start, root_in_idx - 1);
        }
        if root_in_idx < in_end {
            root.borrow_mut().right = helper(pre, in_map, pre_idx, root_in_idx + 1, in_end);
        }
        Some(root)
    }

    helper(&preorder, &in_map, &mut pre_idx, 0, inorder.len() - 1)
}
```
