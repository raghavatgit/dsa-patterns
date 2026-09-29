# 105. Construct Binary Tree from Preorder and Inorder

## Complexity
- Time Complexity: O(n) using hash map index lookups
- Space Complexity: O(n) for recursive tree creation and index table

## Rust Implementation
```rust
use std::collections::HashMap;

pub fn build_tree(preorder: Vec<i32>, inorder: Vec<i32>) -> Option<Rc<RefCell<TreeNode>>> {
    let mut in_map = HashMap::new();
    for (i, &v) in inorder.iter().enumerate() {
        in_map.insert(v, i);
    }
    let mut pre_idx = 0;

    fn construct(
        pre: &Vec<i32>,
        in_map: &HashMap<i32, usize>,
        pre_idx: &mut usize,
        left: usize,
        right: usize
    ) -> Option<Rc<RefCell<TreeNode>>> {
        if left > right { return None; }
        let root_val = pre[*pre_idx];
        *pre_idx += 1;
        let root_in_idx = *in_map.get(&root_val).unwrap();

        let left_child = if root_in_idx > 0 && root_in_idx - 1 >= left {
            construct(pre, in_map, pre_idx, left, root_in_idx - 1)
        } else {
            None
        };
        let right_child = construct(pre, in_map, pre_idx, root_in_idx + 1, right);

        Some(Rc::new(RefCell::new(TreeNode {
            val: root_val,
            left: left_child,
            right: right_child,
        })))
    }

    if preorder.is_empty() { return None; }
    construct(&preorder, &in_map, &mut pre_idx, 0, inorder.len() - 1)
}
```

## TypeScript Implementation
```typescript
export function buildTree(preorder: number[], inorder: number[]): TreeNode | null {
    const map = new Map<number, number>();
    inorder.forEach((val, idx) => map.set(val, idx));
    let preIndex = 0;

    function build(left: number, right: number): TreeNode | null {
        if (left > right) return null;
        const val = preorder[preIndex++];
        const root = new TreeNode(val);
        const mid = map.get(val)!;

        root.left = build(left, mid - 1);
        root.right = build(mid + 1, right);
        return root;
    }

    return build(0, inorder.length - 1);
}
```
