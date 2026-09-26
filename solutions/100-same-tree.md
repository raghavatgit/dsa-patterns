# 100. Same Tree

## Problem Statement
Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

---

## TypeScript Implementation

```typescript
export function isSameTree(p: TreeNode | null, q: TreeNode | null): boolean {
  if (p === null && q === null) return true;
  if (p === null || q === null) return false;
  if (p.val !== q.val) return false;

  return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```

---

## Rust Implementation

```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn is_same_tree(p: Option<Rc<RefCell<TreeNode>>>, q: Option<Rc<RefCell<TreeNode>>>) -> bool {
    match (p, q) {
        (None, None) => true,
        (Some(pn), Some(qn)) => {
            let p_borrow = pn.borrow();
            let q_borrow = qn.borrow();
            p_borrow.val == q_borrow.val
                && is_same_tree(p_borrow.left.clone(), q_borrow.left.clone())
                && is_same_tree(p_borrow.right.clone(), q_borrow.right.clone())
        }
        _ => false,
    }
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) minimum size of both trees.
* **Space Complexity:** O(H) recursion stack height.
