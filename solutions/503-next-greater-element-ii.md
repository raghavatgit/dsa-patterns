# Problem 503: Next Greater Element II

## Problem Statement
Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return the next greater number for every element in `nums`.

## Approach
Simulate circular indexing by iterating from index `0` to `2 * n - 1` with modulo `i % n`.
Maintain a monotonic stack of indices. Only push indices when `i < n`.

## Complexity
- Time: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <stack>

std::vector<int> nextGreaterElements(const std::vector<int>& nums) {
    int n = nums.size();
    std::vector<int> result(n, -1);
    std::stack<int> st;

    for (int i = 0; i < 2 * n; ++i) {
        int val = nums[i % n];
        while (!st.empty() && nums[st.top()] < val) {
            result[st.top()] = val;
            st.pop();
        }
        if (i < n) {
            st.push(i);
        }
    }
    return result;
}
```
