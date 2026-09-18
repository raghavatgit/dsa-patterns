# Problem: Reverse Nodes in k-Group

## Problem Statement
Given the head of a linked list, reverse the nodes of the list `k` at a time, and return the modified list. `k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k`, left-out nodes in the end should remain as-is.
You must solve the problem in $O(1)$ auxiliary memory space without modifying node values.

## Intuition & Approach
Iterative In-Place Sublist Reversal:
1. Count `k` nodes ahead using a check pointer. If fewer than `k` nodes remain, terminate traversal.
2. Maintain `prev_group_end` pointing to the node preceding the current `k`-block.
3. Reverse the sublist of length `k` using standard 3-pointer iterative reversal (`curr`, `next`, `prev`).
4. Reconnect the reversed sublist back to `prev_group_end` and link its new tail to the remaining unreversed list.
5. Advance `prev_group_end` to the new tail of the reversed group.
6. Time Complexity: $O(N)$ with each node visited twice. Space Complexity: $O(1)$ auxiliary pointers.

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

export function reverseKGroup(head: ListNode | null, k: number): ListNode | null {
  if (!head || k <= 1) return head;

  const dummy = new ListNode(0, head);
  let groupPrev: ListNode = dummy;

  while (true) {
    // Verify at least k nodes remain
    let kth: ListNode | null = groupPrev;
    for (let i = 0; i < k && kth !== null; i++) {
      kth = kth.next;
    }
    if (kth === null) break;

    const groupNext = kth.next;
    let prev = groupNext;
    let curr = groupPrev.next;

    // In-place reversal of k nodes
    while (curr !== groupNext && curr !== null) {
      const nxt = curr.next;
      curr.next = prev;
      prev = curr;
      curr = nxt;
    }

    const newGroupEnd = groupPrev.next;
    groupPrev.next = kth;
    groupPrev = newGroupEnd!;
  }

  return dummy.next;
}
```

## Rust Implementation

```rust
#[derive(PartialEq, Eq, Clone, Debug)]
pub struct ListNode {
    pub val: i32,
    pub next: Option<Box<ListNode>>,
}

impl ListNode {
    #[inline]
    pub fn new(val: i32) -> Self {
        ListNode { val, next: None }
    }
}

pub fn reverse_k_group(mut head: Option<Box<ListNode>>, k: i32) -> Option<Box<ListNode>> {
    let mut count = 0;
    let mut curr = head.as_ref();
    while let Some(node) = curr {
        count += 1;
        if count == k { break; }
        curr = node.next.as_ref();
    }

    if count < k {
        return head;
    }

    let mut prev = None;
    let mut curr = head;
    for _ in 0..k {
        if let Some(mut node) = curr {
            let next = node.next.take();
            node.next = prev;
            prev = Some(node);
            curr = next;
        }
    }

    let mut tail = prev.as_mut();
    while let Some(node) = tail {
        if node.next.is_none() {
            node.next = reverse_k_group(curr, k);
            break;
        }
        tail = node.next.as_mut();
    }

    prev
}
```
