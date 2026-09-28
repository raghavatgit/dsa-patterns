# 235. Lowest Common Ancestor of a Binary Search Tree

## Complexity
- Time Complexity: O(h)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn lowest_common_ancestor(
    root: Option<Rc<RefCell<TreeNode>>>,
    p: Option<Rc<RefCell<TreeNode>>>,
    q: Option<Rc<RefCell<TreeNode>>>,
) -> Option<Rc<RefCell<TreeNode>>> {
    let p_val = p.unwrap().borrow().val;
    let q_val = q.unwrap().borrow().val;
    let mut curr = root;

    while let Some(node) = curr {
        let val = node.borrow().val;
        if p_val < val && q_val < val {
            curr = node.borrow().left.clone();
        } else if p_val > val && q_val > val {
            curr = node.borrow().right.clone();
        } else {
            return Some(node);
        }
    }

    None
}
```

## TypeScript Implementation
```typescript
export function lowestCommonAncestor(
    root: TreeNode | null,
    p: TreeNode | null,
    q: TreeNode | null
): TreeNode | null {
    let curr = root;
    while (curr && p && q) {
        if (p.val < curr.val && q.val < curr.val) curr = curr.left;
        else if (p.val > curr.val && q.val > curr.val) curr = curr.right;
        else return curr;
    }
    return null;
}
```
