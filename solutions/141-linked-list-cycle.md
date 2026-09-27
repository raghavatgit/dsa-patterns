# 141. Linked List Cycle

## Problem Statement
Given `head`, the head of a linked list, determine if the linked list has a cycle in it using O(1) memory.

---

## TypeScript Implementation

```typescript
export function hasCycle(head: ListNode | null): boolean {
  if (!head || !head.next) return false;
  let slow: ListNode | null = head;
  let fast: ListNode | null = head;

  while (fast !== null && fast.next !== null) {
    slow = slow!.next;
    fast = fast.next.next;
    if (slow === fast) return true;
  }

  return false;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) fast pointer catches slow pointer within one cycle.
* **Space Complexity:** O(1) two pointers.
