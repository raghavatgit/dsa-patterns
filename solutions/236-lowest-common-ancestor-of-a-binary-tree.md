# 236. Lowest Common Ancestor of a Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn lowest_common_ancestor(
    root: Option<Rc<RefCell<TreeNode>>>,
    p: Option<Rc<RefCell<TreeNode>>>,
    q: Option<Rc<RefCell<TreeNode>>>,
) -> Option<Rc<RefCell<TreeNode>>> {
    let p_target = p.as_ref().map(|n| n.borrow().val);
    let q_target = q.as_ref().map(|n| n.borrow().val);

    fn helper(
        node: Option<Rc<RefCell<TreeNode>>>,
        p_val: Option<i32>,
        q_val: Option<i32>,
    ) -> Option<Rc<RefCell<TreeNode>>> {
        let n = match node {
            Some(curr) => curr,
            None => return None,
        };

        let val = n.borrow().val;
        if Some(val) == p_val || Some(val) == q_val {
            return Some(n);
        }

        let left = helper(n.borrow().left.clone(), p_val, q_val);
        let right = helper(n.borrow().right.clone(), p_val, q_val);

        if left.is_some() && right.is_some() {
            Some(n)
        } else if left.is_some() {
            left
        } else {
            right
        }
    }

    helper(root, p_target, q_target)
}
```

## TypeScript Implementation
```typescript
export function lowestCommonAncestor(
    root: TreeNode | null,
    p: TreeNode | null,
    q: TreeNode | null
): TreeNode | null {
    if (!root || root === p || root === q) return root;
    const left = lowestCommonAncestor(root.left, p, q);
    const right = lowestCommonAncestor(root.right, p, q);
    if (left && right) return root;
    return left || right;
}
```
