# Pattern: Fast and Slow Pointers (Floyd's Tortoise and Hare)

## Core Mechanics
- Move `slow` pointer by 1 step: `slow = slow->next`.
- Move `fast` pointer by 2 steps: `fast = fast->next->next`.

## Applications
1. **Cycle Detection (LeetCode 141)**: If a cycle exists, `fast` and `slow` will collide inside the loop.
2. **Cycle Origin Finding (LeetCode 142)**: After collision, reset `slow` to `head`. Move both 1 step at a time until they meet at cycle entry.
3. **Middle of Linked List (LeetCode 876)**: When `fast` reaches tail, `slow` is at the exact midpoint (essential for Merge Sort and Reorder List).
4. **Happy Number (LeetCode 202)**: Value cycle detection using implicit pointer progression.
