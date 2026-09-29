# 160. Intersection of Two Linked Lists

## Complexity
- Time Complexity: O(m + n)
- Space Complexity: O(1)

## Invariant
Pointer A walks list A then list B. Pointer B walks list B then list A.
Both traverse exactly `len(A) + len(B)` steps, guaranteeing meeting at the intersection node or null.

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
