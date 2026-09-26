# 101. Symmetric Tree

## Problem Statement
Given the `root` of a binary tree, check whether it is a mirror of itself (symmetric around its center).

---

## TypeScript Implementation

```typescript
export function isSymmetric(root: TreeNode | null): boolean {
  if (!root) return true;

  function isMirror(t1: TreeNode | null, t2: TreeNode | null): boolean {
    if (!t1 && !t2) return true;
    if (!t1 || !t2) return false;
    return t1.val === t2.val
      && isMirror(t1.left, t2.right)
      && isMirror(t1.right, t2.left);
  }

  return isMirror(root.left, root.right);
}
```

---

## Rust Implementation

```rust
pub fn is_symmetric(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
    fn is_mirror(
        t1: Option<&Rc<RefCell<TreeNode>>>,
        t2: Option<&Rc<RefCell<TreeNode>>>,
    ) -> bool {
        match (t1, t2) {
            (None, None) => true,
            (Some(n1), Some(n2)) => {
                let b1 = n1.borrow();
                let b2 = n2.borrow();
                b1.val == b2.val
                    && is_mirror(b1.left.as_ref(), b2.right.as_ref())
                    && is_mirror(b1.right.as_ref(), b2.left.as_ref())
            }
            _ => false,
        }
    }

    match root.as_ref() {
        None => true,
        Some(node) => {
            let b = node.borrow();
            is_mirror(b.left.as_ref(), b.right.as_ref())
        }
    }
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) visits each tree node.
* **Space Complexity:** O(H) recursion depth.
