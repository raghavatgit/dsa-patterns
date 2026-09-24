# Problem 023: Merge k Sorted Lists

## Problem Statement
You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order. Merge all the linked-lists into one sorted linked-list and return it.

## Divide and Conquer
Pairwise merge lists:
In round 1, merge $0$ with $1$, $2$ with $3$, etc. Number of lists shrinks by half each round until only 1 remains.

## Complexity
- Time: $O(N \log K)$ where $N$ is total nodes, $K$ is number of lists.
- Space: $O(1)$ auxiliary space.

## C++ Implementation
```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class Solution {
    ListNode* mergeTwo(ListNode* l1, ListNode* l2) {
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
    ListNode* mergeKLists(std::vector<ListNode*>& lists) {
        if (lists.empty()) return nullptr;
        int interval = 1;
        int n = lists.size();
        while (interval < n) {
            for (int i = 0; i + interval < n; i += interval * 2) {
                lists[i] = mergeTwo(lists[i], lists[i + interval]);
            }
            interval *= 2;
        }
        return lists[0];
    }
};
```
