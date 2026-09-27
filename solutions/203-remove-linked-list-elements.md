# 203. Remove Linked List Elements

## Problem Statement
Given the `head` of a linked list and an integer `val`, remove all nodes of the linked list that have `Node.val == val`.

---

## TypeScript Implementation

```typescript
export function removeElements(head: ListNode | null, val: number): ListNode | null {
  const dummy = new ListNode(0, head);
  let curr = dummy;

  while (curr.next !== null) {
    if (curr.next.val === val) {
      curr.next = curr.next.next;
    } else {
      curr = curr.next;
    }
  }

  return dummy.next;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N).
* **Space Complexity:** O(1) in-place.
