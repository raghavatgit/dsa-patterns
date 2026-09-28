# 94. Binary Tree Inorder Traversal

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h) where h is tree height

## Rust Implementation
```rust
#[derive(Debug, PartialEq, Eq)]
pub struct TreeNode {
    pub val: i32,
    pub left: Option<Rc<RefCell<TreeNode>>>,
    pub right: Option<Rc<RefCell<TreeNode>>>,
}

use std::rc::Rc;
use std::cell::RefCell;

pub fn inorder_traversal(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<i32> {
    let mut res = Vec::new();
    let mut stack = Vec::new();
    let mut curr = root;

    while curr.is_some() || !stack.is_empty() {
        while let Some(node) = curr {
            curr = node.borrow().left.clone();
            stack.push(node);
        }
        if let Some(node) = stack.pop() {
            res.push(node.borrow().val);
            curr = node.borrow().right.clone();
        }
    }

    res
}
```

## TypeScript Implementation
```typescript
export class TreeNode {
    val: number;
    left: TreeNode | null;
    right: TreeNode | null;
    constructor(val = 0, left = null, right = null) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

export function inorderTraversal(root: TreeNode | null): number[] {
    const res: number[] = [];
    const stack: TreeNode[] = [];
    let curr = root;

    while (curr || stack.length > 0) {
        while (curr) {
            stack.push(curr);
            curr = curr.left;
        }
        curr = stack.pop()!;
        res.push(curr.val);
        curr = curr.right;
    }

    return res;
}
```
