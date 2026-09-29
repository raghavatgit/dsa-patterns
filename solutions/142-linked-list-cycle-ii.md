# 142. Linked List Cycle II

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Invariant
Let distance to cycle start be `a`, distance from start to meeting point `b`, remaining cycle `c`.
Fast distance = `2 * slow distance` => `a + b + k*(b+c) = 2(a + b)` => `a = k*(b+c) - b = (k-1)*(b+c) + c`.
Resetting one pointer to head and moving both at speed 1 guarantees intersection at cycle start.

## TypeScript Implementation
```typescript
export function detectCycle(head: ListNode | null): ListNode | null {
    let slow = head;
    let fast = head;

    while (fast && fast.next) {
        slow = slow!.next;
        fast = fast.next.next;
        if (slow === fast) {
            let ptr1 = head;
            let ptr2 = slow;
            while (ptr1 !== ptr2) {
                ptr1 = ptr1!.next;
                ptr2 = ptr2!.next;
            }
            return ptr1;
        }
    }
    return null;
}
```
