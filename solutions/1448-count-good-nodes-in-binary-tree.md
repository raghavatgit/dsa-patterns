# 1448. Count Good Nodes in Binary Tree

## Problem Statement
Given a binary tree `root`, a node `X` in the tree is named **good** if in the path from the root to `X` there are no nodes with a value greater than `X`.

Return the number of **good** nodes in the binary tree.

---

## TypeScript Implementation

```typescript
export class TreeNode {
  val: number;
  left: TreeNode | null;
  right: TreeNode | null;
  constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
    this.val = val === undefined ? 0 : val;
    this.left = left === undefined ? null : left;
    this.right = right === undefined ? null : right;
  }
}

export function goodNodes(root: TreeNode | null): number {
  if (!root) return 0;

  let goodCount = 0;

  function dfs(node: TreeNode | null, maxVal: number): void {
    if (!node) return;

    if (node.val >= maxVal) {
      goodCount++;
      maxVal = node.val;
    }

    dfs(node.left, maxVal);
    dfs(node.right, maxVal);
  }

  dfs(root, root.val);
  return goodCount;
}
```

---

## Rust Implementation

```rust
use std::rc::Rc;
use std::cell::RefCell;

#[derive(Debug, PartialEq, Eq)]
pub struct TreeNode {
    pub val: i32,
    pub left: Option<Rc<RefCell<TreeNode>>>,
    pub right: Option<Rc<RefCell<TreeNode>>>,
}

pub struct Solution;

impl Solution {
    pub fn good_nodes(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
        fn dfs(node: Option<Rc<RefCell<TreeNode>>>, mut max_val: i32) -> i32 {
            match node {
                None => 0,
                Some(n) => {
                    let n_borrow = n.borrow();
                    let mut count = 0;
                    if n_borrow.val >= max_val {
                        count += 1;
                        max_val = n_borrow.val;
                    }
                    count + dfs(n_borrow.left.clone(), max_val) + dfs(n_borrow.right.clone(), max_val)
                }
            }
        }

        match &root {
            None => 0,
            Some(n) => dfs(root.clone(), n.borrow().val),
        }
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(n)` where `n` is the number of nodes in the binary tree.
- Space Complexity: `O(h)` call stack space where `h` is the tree height (`O(log n)` for balanced, `O(n)` for degenerated tree).
