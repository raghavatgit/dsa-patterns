# 114. Flatten Binary Tree to Linked List

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1) using Morris predecessor wiring

## Rust Implementation
```rust
pub fn flatten(root: &mut Option<Rc<RefCell<TreeNode>>>) {
    let mut curr = root.clone();
    while let Some(node) = curr {
        let mut b = node.borrow_mut();
        if let Some(left) = b.left.take() {
            let mut rightmost = left.clone();
            loop {
                let next = rightmost.borrow().right.clone();
                match next {
                    Some(n) => rightmost = n,
                    None => break,
                }
            }
            rightmost.borrow_mut().right = b.right.take();
            b.right = Some(left);
        }
        curr = b.right.clone();
    }
}
```

## TypeScript Implementation
```typescript
export function flatten(root: TreeNode | null): void {
    let curr = root;
    while (curr) {
        if (curr.left) {
            let rightmost = curr.left;
            while (rightmost.right) {
                rightmost = rightmost.right;
            }
            rightmost.right = curr.right;
            curr.right = curr.left;
            curr.left = null;
        }
        curr = curr.right;
    }
}
```
