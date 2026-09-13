# Binary Tree Traversals (DFS & BFS)

## Concept
Binary tree traversals systematically visit each node in a hierarchical structure. They form the foundation for syntax tree evaluation, hierarchical layout rendering, and prefix search trees.

* **Depth-First Search (DFS):**
  * **Preorder (Root -> Left -> Right):** Serializing and cloning tree structures.
  * **Inorder (Left -> Root -> Right):** Yields sorted order in Binary Search Trees (BST).
  * **Postorder (Left -> Right -> Root):** Bottom-up dependency resolution and memory freeing.
* **Breadth-First Search (BFS / Level Order):** Visits nodes level-by-level using a FIFO queue.

## TypeScript Implementation

```typescript
export class TreeNode {
  val: number;
  left: TreeNode | null;
  right: TreeNode | null;

  constructor(val: number, left: TreeNode | null = null, right: TreeNode | null = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

// Inorder traversal: Left -> Root -> Right
export function inorderTraversal(root: TreeNode | null): number[] {
  const result: number[] = [];
  const stack: TreeNode[] = [];
  let curr = root;

  while (curr !== null || stack.length > 0) {
    while (curr !== null) {
      stack.push(curr);
      curr = curr.left;
    }
    curr = stack.pop()!;
    result.push(curr.val);
    curr = curr.right;
  }

  return result;
}

// Level-order traversal (BFS)
export function levelOrder(root: TreeNode | null): number[][] {
  if (!root) return [];
  const levels: number[][] = [];
  const queue: TreeNode[] = [root];

  while (queue.length > 0) {
    const levelSize = queue.length;
    const currentLevel: number[] = [];

    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift()!;
      currentLevel.push(node.val);

      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    levels.push(currentLevel);
  }

  return levels;
}
```

## Rust Implementation

```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;

#[derive(Debug, PartialEq, Eq)]
pub struct TreeNode {
    pub val: i32,
    pub left: Option<Rc<RefCell<TreeNode>>>,
    pub right: Option<Rc<RefCell<TreeNode>>>,
}

impl TreeNode {
    pub fn new(val: i32) -> Self {
        TreeNode { val, left: None, right: None }
    }
}

pub fn level_order(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<Vec<i32>> {
    let mut result = Vec::new();
    let root = match root {
        Some(r) => r,
        None => return result,
    };

    let mut queue = VecDeque::new();
    queue.push_back(root);

    while !queue.is_empty() {
        let level_size = queue.len();
        let mut current_level = Vec::with_capacity(level_size);

        for _ in 0..level_size {
            if let Some(node) = queue.pop_front() {
                let n = node.borrow();
                current_level.push(n.val);

                if let Some(ref left) = n.left {
                    queue.push_back(Rc::clone(left));
                }
                if let Some(ref right) = n.right {
                    queue.push_back(Rc::clone(right));
                }
            }
        }
        result.push(current_level);
    }

    result
}
```

## Complexity Analysis
* **Time Complexity:** O(N) where N is the total number of nodes, as every node is visited exactly once.
* **Space Complexity:** O(H) stack space for DFS where H is tree height; O(W) queue space for BFS where W is maximum tree width.
