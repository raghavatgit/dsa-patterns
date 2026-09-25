# Problem 143: Reorder List

## Problem Statement
You are given the head of a singly linked-list:
$L_0 \to L_1 \to \dots \to L_{n - 1} \to L_n$
Reorder the list to be:
$L_0 \to L_n \to L_1 \to L_{n - 1} \to L_2 \to L_{n - 2} \to \dots$
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

## Three-Step Algorithm
1. **Find Middle**: Fast and slow pointer Floyd traversal to partition into two halves.
2. **Reverse Second Half**: Standard in-place 3-pointer iterative reversal.
3. **Interleave**: Alternately merge nodes from first half and reversed second half.

## Complexity
- Time: $O(N)$
- Space: $O(1)$

## C++ Implementation
```cpp
void reorderList(ListNode* head) {
    if (!head || !head->next) return;

    // Step 1: Find middle using fast and slow pointers
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast->next && fast->next->next) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // Step 2: Reverse second half
    ListNode* prev = nullptr;
    ListNode* curr = slow->next;
    slow->next = nullptr; // Split lists

    while (curr) {
        ListNode* nextTemp = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextTemp;
    }

    // Step 3: Interleave first half (head) and reversed second half (prev)
    ListNode* first = head;
    ListNode* second = prev;

    while (second) {
        ListNode* t1 = first->next;
        ListNode* t2 = second->next;

        first->next = second;
        second->next = t1;

        first = t1;
        second = t2;
    }
}
```
