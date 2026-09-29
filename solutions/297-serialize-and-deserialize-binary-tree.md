# 297. Serialize and Deserialize Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub struct Codec;

impl Codec {
    pub fn new() -> Self { Self }

    pub fn serialize(&self, root: Option<Rc<RefCell<TreeNode>>>) -> String {
        let mut out = Vec::new();
        fn dfs(node: Option<Rc<RefCell<TreeNode>>>, out: &mut Vec<String>) {
            match node {
                None => out.push("N".to_string()),
                Some(n) => {
                    out.push(n.borrow().val.to_string());
                    dfs(n.borrow().left.clone(), out);
                    dfs(n.borrow().right.clone(), out);
                }
            }
        }
        dfs(root, &mut out);
        out.join(",")
    }
}
```
