# 021. Merge Two Sorted Lists

## Problem Statement
You are given the heads of two sorted linked lists `list1` and `list2`. Merge the two lists into one sorted list by splicing together nodes of the initial two lists.

---

## TypeScript Implementation

```typescript
export function mergeTwoLists(l1: ListNode | null, l2: ListNode | null): ListNode | null {
  const dummy = new ListNode(0);
  let tail = dummy;

  while (l1 !== null && l2 !== null) {
    if (l1.val <= l2.val) {
      tail.next = l1;
      l1 = l1.next;
    } else {
      tail.next = l2;
      l2 = l2.next;
    }
    tail = tail.next;
  }

  tail.next = l1 !== null ? l1 : l2;
  return dummy.next;
}
```

---

## Rust Implementation

```rust
pub fn merge_two_lists(
    mut l1: Option<Box<ListNode>>,
    mut l2: Option<Box<ListNode>>,
) -> Option<Box<ListNode>> {
    let mut dummy = ListNode::new(0);
    let mut tail = &mut dummy;

    while l1.is_some() && l2.is_some() {
        if l1.as_ref().unwrap().val <= l2.as_ref().unwrap().val {
            let next = l1.as_mut().unwrap().next.take();
            tail.next = l1;
            l1 = next;
        } else {
            let next = l2.as_mut().unwrap().next.take();
            tail.next = l2;
            l2 = next;
        }
        tail = tail.next.as_mut().unwrap();
    }

    tail.next = if l1.is_some() { l1 } else { l2 };
    dummy.next
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N + M) where N and M are the lengths of list1 and list2.
* **Space Complexity:** O(1) in-place pointer manipulation.
