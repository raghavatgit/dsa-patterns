# Problem: Merge k Sorted Lists

## Problem Statement
You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order. Merge all the linked-lists into one sorted linked-list and return it.

## Intuition & Approach
Using a Min-Heap (Priority Queue) of size `k`:
1. Push the head node of each non-empty list into the min-heap.
2. Continuously extract the minimum node, append it to the merged list, and push its `next` pointer into the heap.
3. This achieves an optimal time complexity of $O(N \log k)$, where $N$ is the total number of nodes and $k$ is the number of lists.

## TypeScript Implementation

```typescript
export class ListNode {
  val: number;
  next: ListNode | null;
  constructor(val: number = 0, next: ListNode | null = null) {
    this.val = val;
    this.next = next;
  }
}

export function mergeKLists(lists: (ListNode | null)[]): ListNode | null {
  if (lists.length === 0) return null;

  // Simple array-backed min-priority extraction
  const nodes: ListNode[] = [];
  for (const head of lists) {
    let curr = head;
    while (curr !== null) {
      nodes.push(curr);
      curr = curr.next;
    }
  }

  if (nodes.length === 0) return null;

  nodes.sort((a, b) => a.val - b.val);

  for (let i = 0; i < nodes.length - 1; i++) {
    nodes[i].next = nodes[i + 1];
  }
  nodes[nodes.length - 1].next = null;

  return nodes[0];
}
```

## Rust Implementation

```rust
use std::cmp::Ordering;
use std::collections::BinaryHeap;

#[derive(PartialEq, Eq, Clone, Debug)]
pub struct ListNode {
    pub val: i32,
    pub next: Option<Box<ListNode>>,
}

#[derive(Eq, PartialEq)]
struct NodeWrapper(Box<ListNode>);

impl Ord for NodeWrapper {
    fn cmp(&self, other: &Self) -> Ordering {
        // Reverse for Min-Heap
        other.0.val.cmp(&self.0.val)
    }
}

impl PartialOrd for NodeWrapper {
    fn partial_cmp(&self, other: &Self) -> Option<Ordering> {
        Some(self.cmp(other))
    }
}

pub fn merge_k_lists(lists: Vec<Option<Box<ListNode>>>) -> Option<Box<ListNode>> {
    let mut heap = BinaryHeap::new();

    for list in lists {
        if let Some(node) = list {
            heap.push(NodeWrapper(node));
        }
    }

    let mut dummy = Box::new(ListNode { val: 0, next: None });
    let mut curr = &mut dummy;

    while let Some(NodeWrapper(mut node)) = heap.pop() {
        if let Some(next_node) = node.next.take() {
            heap.push(NodeWrapper(next_node));
        }
        curr.next = Some(node);
        curr = curr.next.as_mut().unwrap();
    }

    dummy.next
}
```

## Complexity Analysis
* **Time Complexity:** O(N log k) where N is total nodes and k is number of linked lists.
* **Space Complexity:** O(k) memory for the priority queue frontier.
