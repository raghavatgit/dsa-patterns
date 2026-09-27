# 083. Remove Duplicates from Sorted List

## Problem Statement
Given the `head` of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

---

## TypeScript Implementation

```typescript
export function deleteDuplicates(head: ListNode | null): ListNode | null {
  let curr = head;
  while (curr !== null && curr.next !== null) {
    if (curr.val === curr.next.val) {
      curr.next = curr.next.next;
    } else {
      curr = curr.next;
    }
  }
  return head;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) single pass.
* **Space Complexity:** O(1) in-place.
