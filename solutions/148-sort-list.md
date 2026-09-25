# Problem 148: Sort List

## Problem Statement
Given the head of a linked list, return the list after sorting it in ascending order in $O(N \log N)$ time and $O(\log N)$ recursion stack space.

## Merge Sort on Linked List
1. Partition list into two halves using fast and slow pointers.
2. Recursively sort `left` and `right` sublists.
3. Merge two sorted lists using dummy head in $O(N)$ time.

## Complexity
- Time: $O(N \log N)$
- Space: $O(\log N)$ recursion stack

## C++ Implementation
```cpp
class Solution {
    ListNode* merge(ListNode* l1, ListNode* l2) {
        ListNode dummy(0);
        ListNode* tail = &dummy;

        while (l1 && l2) {
            if (l1->val <= l2->val) {
                tail->next = l1;
                l1 = l1->next;
            } else {
                tail->next = l2;
                l2 = l2->next;
            }
            tail = tail->next;
        }
        tail->next = l1 ? l1 : l2;
        return dummy.next;
    }

public:
    ListNode* sortList(ListNode* head) {
        if (!head || !head->next) return head;

        ListNode* prev = nullptr;
        ListNode* slow = head;
        ListNode* fast = head;

        while (fast && fast->next) {
            prev = slow;
            slow = slow->next;
            fast = fast->next->next;
        }

        prev->next = nullptr; // Split into two halves

        ListNode* l1 = sortList(head);
        ListNode* l2 = sortList(slow);
        return merge(l1, l2);
    }
};
```
