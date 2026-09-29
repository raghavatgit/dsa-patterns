# 23. Merge K Sorted Lists

## Complexity
- Time Complexity: O(N log k)
- Space Complexity: O(k)

## TypeScript Implementation
```typescript
export function mergeKLists(lists: Array<ListNode | null>): ListNode | null {
    if (lists.length === 0) return null;
    let step = 1;
    while (step < lists.length) {
        for (let i = 0; i + step < lists.length; i += step * 2) {
            lists[i] = mergeTwoLists(lists[i], lists[i + step]);
        }
        step *= 2;
    }
    return lists[0];
}
```
