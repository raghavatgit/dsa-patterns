# Problem: Reverse Linked List

## Problem Statement
Given the `head` of a singly linked list, reverse the list, and return the reversed list.

## Intuition & Approach
* **Iterative Approach:** Maintain three pointers: `prev = null`, `curr = head`, and `next = curr.next`. Invert `curr.next = prev`, then advance `prev` and `curr`.
* **Recursive Approach:** Recursively reverse the rest of the list `rest = reverse(head.next)`. Point `head.next.next = head` and sever `head.next = null`.

## C Implementation

```c
#include <stdlib.h>

struct ListNode {
    int val;
    struct ListNode* next;
};

struct ListNode* reverseList(struct ListNode* head) {
    struct ListNode* prev = NULL;
    struct ListNode* curr = head;

    while (curr != NULL) {
        struct ListNode* nextTemp = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextTemp;
    }

    return prev;
}
```

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

export function reverseList(head: ListNode | null): ListNode | null {
  let prev: ListNode | null = null;
  let curr: ListNode | null = head;

  while (curr !== null) {
    const nextTemp: ListNode | null = curr.next;
    curr.next = prev;
    prev = curr;
    curr = nextTemp;
  }

  return prev;
}
```

## Complexity Analysis
* **Time Complexity:** O(N) visits each node once.
* **Space Complexity:** O(1) iterative in-place pointer swapping.
