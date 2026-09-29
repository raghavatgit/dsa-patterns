# 138. Copy List with Random Pointer

## Complexity
- Time Complexity: O(n) three-pass interweaving
- Space Complexity: O(1) auxiliary space

## TypeScript Implementation
```typescript
export function copyRandomList(head: Node | null): Node | null {
    if (!head) return null;

    // Step 1: Interweave cloned nodes
    let curr: Node | null = head;
    while (curr) {
        const next: Node | null = curr.next;
        const clone = new Node(curr.val);
        curr.next = clone;
        clone.next = next;
        curr = next;
    }

    // Step 2: Assign random pointers
    curr = head;
    while (curr) {
        if (curr.random) {
            curr.next!.random = curr.random.next;
        }
        curr = curr.next!.next;
    }

    // Step 3: Unweave the lists
    curr = head;
    const dummy = new Node(0);
    let copyCurr = dummy;
    while (curr) {
        const copyNode = curr.next!;
        curr.next = copyNode.next;
        copyCurr.next = copyNode;
        copyCurr = copyNode;
        curr = curr.next;
    }

    return dummy.next;
}
```
