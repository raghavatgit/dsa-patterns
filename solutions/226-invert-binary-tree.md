# 226. Invert Binary Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(h)

## Rust Implementation
```rust
pub fn invert_tree(root: Option<Rc<RefCell<TreeNode>>>) -> Option<Rc<RefCell<TreeNode>>> {
    if let Some(node) = root.clone() {
        let left = node.borrow().left.clone();
        let right = node.borrow().right.clone();
        node.borrow_mut().left = invert_tree(right);
        node.borrow_mut().right = invert_tree(left);
    }
    root
}
```

## TypeScript Implementation
```typescript
export function invertTree(root: TreeNode | null): TreeNode | null {
    if (!root) return null;
    const temp = root.left;
    root.left = invertTree(root.right);
    root.right = invertTree(temp);
    return root;
}
```
