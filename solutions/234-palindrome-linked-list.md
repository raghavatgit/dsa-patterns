# 234. Palindrome Linked List

## Problem Statement
Given the `head` of a singly linked list, return `true` if it is a palindrome with O(1) extra space.

---

## Midpoint & Reverse Technique
1. Use fast/slow pointers to locate list midpoint.
2. In-place reverse the second half.
3. Compare first half against reversed second half.

---

## TypeScript Implementation

```typescript
export function isPalindrome(head: ListNode | null): boolean {
  if (!head || !head.next) return true;

  // Find midpoint
  let slow = head, fast = head;
  while (fast.next !== null && fast.next.next !== null) {
    slow = slow.next!;
    fast = fast.next.next;
  }

  // Reverse second half
  let prev: ListNode | null = null;
  let curr = slow.next;
  while (curr !== null) {
    const next = curr.next;
    curr.next = prev;
    prev = curr;
    curr = next;
  }

  // Compare
  let p1: ListNode | null = head;
  let p2: ListNode | null = prev;
  while (p2 !== null) {
    if (p1!.val !== p2.val) return false;
    p1 = p1!.next;
    p2 = p2.next;
  }

  return true;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N).
* **Space Complexity:** O(1) in-place.
