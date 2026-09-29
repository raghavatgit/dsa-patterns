# 98. Validate Binary Search Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h) recursion stack where h is tree height

## Invariants
Every node value must satisfy `low < node.val < high`. The left subtree inherits `(low, node.val)` and the right subtree inherits `(node.val, high)`.

## Rust Implementation
```rust
use std::rc::Rc;
use std::cell::RefCell;

pub fn is_valid_bst(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
    fn validate(node: &Option<Rc<RefCell<TreeNode>>>, min_val: Option<i64>, max_val: Option<i64>) -> bool {
        match node {
            None => true,
            Some(n) => {
                let n_borrow = n.borrow();
                let val = n_borrow.val as i64;
                if let Some(min) = min_val {
                    if val <= min { return false; }
                }
                if let Some(max) = max_val {
                    if val >= max { return false; }
                }
                validate(&n_borrow.left, min_val, Some(val)) && validate(&n_borrow.right, Some(val), max_val)
            }
        }
    }
    validate(&root, None, None)
}
```

## TypeScript Implementation
```typescript
export function isValidBST(root: TreeNode | null): boolean {
    function validate(node: TreeNode | null, low: number, high: number): boolean {
        if (!node) return true;
        if (node.val <= low || node.val >= high) return false;
        return validate(node.left, low, node.val) && validate(node.right, node.val, high);
    }
    return validate(root, -Infinity, Infinity);
}
```
