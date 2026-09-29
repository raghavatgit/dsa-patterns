# 108. Convert Sorted Array to Binary Search Tree

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(log n) stack frames

## Rust Implementation
```rust
pub fn sorted_array_to_bst(nums: Vec<i32>) -> Option<Rc<RefCell<TreeNode>>> {
    fn helper(arr: &[i32]) -> Option<Rc<RefCell<TreeNode>>> {
        if arr.is_empty() { return None; }
        let mid = arr.len() / 2;
        let mut node = TreeNode::new(arr[mid]);
        node.left = helper(&arr[..mid]);
        node.right = helper(&arr[mid + 1..]);
        Some(Rc::new(RefCell::new(node)))
    }
    helper(&nums)
}
```

## TypeScript Implementation
```typescript
export function sortedArrayToBST(nums: number[]): TreeNode | null {
    function build(start: number, end: number): TreeNode | null {
        if (start > end) return null;
        const mid = Math.floor((start + end) / 2);
        const root = new TreeNode(nums[mid]);
        root.left = build(start, mid - 1);
        root.right = build(mid + 1, end);
        return root;
    }
    return build(0, nums.length - 1);
}
```
