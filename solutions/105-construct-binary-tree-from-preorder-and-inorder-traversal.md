# 105. Construct Binary Tree from Preorder and Inorder Traversal

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::collections::HashMap;

pub fn build_tree(preorder: Vec<i32>, inorder: Vec<i32>) -> Option<Rc<RefCell<TreeNode>>> {
    let mut map = HashMap::new();
    for (i, &v) in inorder.iter().enumerate() {
        map.insert(v, i);
    }

    fn helper(
        preorder: &[i32],
        pre_idx: &mut usize,
        in_start: usize,
        in_end: usize,
        map: &HashMap<i32, usize>,
    ) -> Option<Rc<RefCell<TreeNode>>> {
        if in_start > in_end {
            return None;
        }

        let val = preorder[*pre_idx];
        *pre_idx += 1;
        let root = Rc::new(RefCell::new(TreeNode::new(val)));
        let in_idx = *map.get(&val).unwrap();

        if in_idx > 0 && in_start <= in_idx - 1 {
            root.borrow_mut().left = helper(preorder, pre_idx, in_start, in_idx - 1, map);
        }
        root.borrow_mut().right = helper(preorder, pre_idx, in_idx + 1, in_end, map);

        Some(root)
    }

    let mut pre_idx = 0;
    helper(&preorder, &mut pre_idx, 0, inorder.len() - 1, &map)
}
```

## TypeScript Implementation
```typescript
export function buildTree(preorder: number[], inorder: number[]): TreeNode | null {
    const map = new Map<number, number>();
    inorder.forEach((val, idx) => map.set(val, idx));
    let preIdx = 0;

    const build = (start: number, end: number): TreeNode | null => {
        if (start > end) return null;
        const val = preorder[preIdx++];
        const root = new TreeNode(val);
        const idx = map.get(val)!;

        root.left = build(start, idx - 1);
        root.right = build(idx + 1, end);
        return root;
    };

    return build(0, inorder.length - 1);
}
```
