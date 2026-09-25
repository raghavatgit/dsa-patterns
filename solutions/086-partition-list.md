# Problem 086: Partition List

## Problem Statement
Given the head of a linked list and a value `x`, partition it such that all nodes less than `x` come before nodes greater than or equal to `x`. Preserve the original relative order of the nodes in each of the two partitions.

## Approach
Maintain two separate lists:
1. `less_head` for elements $< x$
2. `greater_head` for elements $\ge x$
Traverse the original list, distribute nodes, terminate `greater_tail->next = nullptr`, and link `less_tail->next = greater_head.next`.

## Complexity
- Time: $O(N)$
- Space: $O(1)$

## C++ Implementation
```cpp
ListNode* partition(ListNode* head, int x) {
    ListNode lessDummy(0);
    ListNode greaterDummy(0);

    ListNode* less = &lessDummy;
    ListNode* greater = &greaterDummy;

    while (head) {
        if (head->val < x) {
            less->next = head;
            less = less->next;
        } else {
            greater->next = head;
            greater = greater->next;
        }
        head = head->next;
    }

    greater->next = nullptr;
    less->next = greaterDummy.next;
    return lessDummy.next;
}
```
