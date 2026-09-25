# Problem 061: Rotate List

## Problem Statement
Given the head of a linked list, rotate the list to the right by `k` places.

## Approach
1. Traverse list to determine length $N$ and locate the tail node.
2. Form a circular ring by linking `tail->next = head`.
3. Normalize rotation: `k = k % N`. If `k == 0`, break ring and return `head`.
4. Traverse $N - k$ steps from tail to find the new tail.
5. Set `new_head = new_tail->next`, break ring `new_tail->next = nullptr`.

## Complexity
- Time: $O(N)$
- Space: $O(1)$

## C++ Implementation
```cpp
ListNode* rotateRight(ListNode* head, int k) {
    if (!head || !head->next || k == 0) return head;

    int length = 1;
    ListNode* tail = head;
    while (tail->next) {
        tail = tail->next;
        length++;
    }

    k = k % length;
    if (k == 0) return head;

    // Connect into a circular linked list
    tail->next = head;

    // Find new tail: length - k steps from start
    int stepsToNewTail = length - k;
    ListNode* newTail = tail;
    while (stepsToNewTail--) {
        newTail = newTail->next;
    }

    ListNode* newHead = newTail->next;
    newTail->next = nullptr;
    return newHead;
}
```
