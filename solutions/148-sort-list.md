# 148. Sort List

## Complexity
- Time Complexity: O(n log n)
- Space Complexity: O(log n) recursion stack

## TypeScript Implementation
```typescript
export function sortList(head: ListNode | null): ListNode | null {
    if (!head || !head.next) return head;

    let prev: ListNode | null = null;
    let slow: ListNode | null = head;
    let fast: ListNode | null = head;

    while (fast && fast.next) {
        prev = slow;
        slow = slow!.next;
        fast = fast.next.next;
    }
    prev!.next = null;

    const l1 = sortList(head);
    const l2 = sortList(slow);
    return merge(l1, l2);
}

function merge(l1: ListNode | null, l2: ListNode | null): ListNode | null {
    const dummy = new ListNode(0);
    let curr = dummy;
    while (l1 && l2) {
        if (l1.val <= l2.val) {
            curr.next = l1;
            l1 = l1.next;
        } else {
            curr.next = l2;
            l2 = l2.next;
        }
        curr = curr.next;
    }
    curr.next = l1 || l2;
    return dummy.next;
}
```
