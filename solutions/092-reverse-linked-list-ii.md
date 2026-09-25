# Problem 092: Reverse Linked List II

## Problem Statement
Given the head of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return the reversed list.

## Single-Pass In-Place Algorithm
Position a pointer `prev` at node `left - 1`.
`curr = prev->next` points to the start of the reversal sublist.
For `right - left` iterations:
- `temp = curr->next`
- `curr->next = temp->next`
- `temp->next = prev->next`
- `prev->next = temp`

## Complexity
- Time: $O(N)$ single pass
- Space: $O(1)$

## C++ Implementation
```cpp
ListNode* reverseBetween(ListNode* head, int left, int right) {
    if (!head || left == right) return head;

    ListNode dummy(0);
    dummy.next = head;
    ListNode* prev = &dummy;

    for (int i = 1; i < left; ++i) {
        prev = prev->next;
    }

    ListNode* curr = prev->next;
    for (int i = 0; i < right - left; ++i) {
        ListNode* temp = curr->next;
        curr->next = temp->next;
        temp->next = prev->next;
        prev->next = temp;
    }

    return dummy.next;
}
```
