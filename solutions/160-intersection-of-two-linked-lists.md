# 160. Intersection of Two Linked Lists

## Problem Statement
Given the heads of two singly linked-lists `headA` and `headB`, return the node at which the two lists intersect.

---

## Dual Pointer Traversal
Pointer A traverses list A then swaps to head B. Pointer B traverses list B then swaps to head A. Both pointers travel identical total distance `len(A) + len(B)`, intersecting at the joint node in O(1) space.

---

## TypeScript Implementation

```typescript
export function getIntersectionNode(headA: ListNode | null, headB: ListNode | null): ListNode | null {
  if (!headA || !headB) return null;
  let pA: ListNode | null = headA;
  let pB: ListNode | null = headB;

  while (pA !== pB) {
    pA = pA === null ? headB : pA.next;
    pB = pB === null ? headA : pB.next;
  }

  return pA;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N + M).
* **Space Complexity:** O(1) zero allocation.
