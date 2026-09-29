# 143. Reorder List

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Method
1. Find middle node using slow and fast pointers.
2. Reverse second half of linked list.
3. Interweave the two halves.

## TypeScript Implementation
```typescript
export function reorderList(head: ListNode | null): void {
    if (!head || !head.next) return;

    let slow: ListNode | null = head;
    let fast: ListNode | null = head;
    while (fast && fast.next) {
        slow = slow!.next;
        fast = fast.next.next;
    }

    let prev: ListNode | null = null;
    let curr: ListNode | null = slow!.next;
    slow!.next = null;
    while (curr) {
        const next: ListNode | null = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }

    let first: ListNode | null = head;
    let second: ListNode | null = prev;
    while (second) {
        const tmp1: ListNode | null = first!.next;
        const tmp2: ListNode | null = second.next;
        first!.next = second;
        second.next = tmp1;
        first = tmp1;
        second = tmp2;
    }
}
```
