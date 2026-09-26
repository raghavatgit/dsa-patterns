# 019. Remove Nth Node From End of List

## Problem Statement
Given the `head` of a linked list, remove the `n`-th node from the end of the list and return its head.

---

## Two-Pointer Gap Technique
Maintain two pointers separated by an `n + 1` node gap. Advance both pointers until the leader hits `null`. The trailing pointer will then stand exactly on the node preceding the target removal node.

---

## TypeScript Implementation

```typescript
class ListNode {
  val: number;
  next: ListNode | null;
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

export function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
  const dummy = new ListNode(0, head);
  let fast: ListNode | null = dummy;
  let slow: ListNode | null = dummy;

  for (let i = 0; i <= n; i++) {
    if (!fast) return head;
    fast = fast.next;
  }

  while (fast !== null) {
    fast = fast.next;
    slow = slow!.next;
  }

  slow!.next = slow!.next!.next;
  return dummy.next;
}
```

---

## Rust Implementation

```rust
#[derive(PartialEq, Eq, Clone, Debug)]
pub struct ListNode {
    pub val: i32,
    pub next: Option<Box<ListNode>>,
}

impl ListNode {
    pub fn new(val: i32) -> Self {
        ListNode { next: None, val }
    }
}

pub fn remove_nth_from_end(head: Option<Box<ListNode>>, n: i32) -> Option<Box<ListNode>> {
    let mut dummy = Some(Box::new(ListNode { val: 0, next: head }));
    let mut len = 0;
    
    {
        let mut curr = dummy.as_ref();
        while let Some(node) = curr {
            curr = node.next.as_ref();
            len += 1;
        }
    }

    let target_idx = len - n - 1;
    let mut curr = dummy.as_mut();

    for _ in 0..target_idx {
        curr = curr.unwrap().next.as_mut();
    }

    let next_node = curr.as_mut().unwrap().next.as_mut().unwrap().next.take();
    curr.as_mut().unwrap().next = next_node;

    dummy.unwrap().next
}
```

---

## Complexity Analysis
* **Time Complexity:** O(L) single pass where L is the list length.
* **Space Complexity:** O(1) auxiliary space.
