# Problem: Binary Tree Maximum Path Sum

## Problem Statement
A path in a binary tree is a sequence of nodes where each pair of adjacent nodes has an edge connecting them. A node can only appear in the sequence at most once. The path does not need to pass through the root. Return the maximum path sum of any non-empty path.

## Intuition & Approach
Post-order Tree Dynamic Programming:
1. For each node, compute the maximum branch sum extending downwards to at most one child: `gain(node) = max(0, node.val + max(gain(left), gain(right)))`.
2. Negative gains are clamped to 0 because omitting a negative child branch improves the total sum.
3. At the current node, the maximum path that turns through this node is `node.val + left_gain + right_gain`. Update the global maximum with this value.
4. Return `node.val + max(left_gain, right_gain)` to the parent caller.
5. Time Complexity: $O(N)$ visiting each node once. Space Complexity: $O(H)$ recursion stack depth.

## TypeScript Implementation

```typescript
export class TreeNode {
  val: number;
  left: TreeNode | null;
  right: TreeNode | null;
  constructor(val: number = 0, left: TreeNode | null = null, right: TreeNode | null = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

export function maxPathSum(root: TreeNode | null): number {
  let maxSum = -Infinity;

  function maxGain(node: TreeNode | null): number {
    if (node === null) return 0;

    const leftGain = Math.max(0, maxGain(node.left));
    const rightGain = Math.max(0, maxGain(node.right));

    const pathSumThroughNode = node.val + leftGain + rightGain;
    if (pathSumThroughNode > maxSum) {
      maxSum = pathSumThroughNode;
    }

    return node.val + Math.max(leftGain, rightGain);
  }

  maxGain(root);
  return maxSum;
}
```

## Rust Implementation

```rust
use std::rc::Rc;
use std::cell::RefCell;

#[derive(Debug, PartialEq, Eq)]
pub struct TreeNode {
    pub val: i32,
    pub left: Option<Rc<RefCell<TreeNode>>>,
    pub right: Option<Rc<RefCell<TreeNode>>>,
}

pub fn max_path_sum(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    let mut max_sum = i32::MIN;

    fn max_gain(node: &Option<Rc<RefCell<TreeNode>>>, max_sum: &mut i32) -> i32 {
        match node {
            None => 0,
            Some(n) => {
                let borrowed = n.borrow();
                let left_gain = max_gain(&borrowed.left, max_sum).max(0);
                let right_gain = max_gain(&borrowed.right, max_sum).max(0);

                let current_path = borrowed.val + left_gain + right_gain;
                *max_sum = (*max_sum).max(current_path);

                borrowed.val + left_gain.max(right_gain)
            }
        }
    }

    max_gain(&root, &mut max_sum);
    max_sum
}
```
