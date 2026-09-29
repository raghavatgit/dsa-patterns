# 141. Linked List Cycle

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## TypeScript Implementation
```typescript
export function hasCycle(head: ListNode | null): boolean {
    let slow = head;
    let fast = head;
    while (fast && fast.next) {
        slow = slow!.next;
        fast = fast.next.next;
        if (slow === fast) return true;
    }
    return false;
}
```
