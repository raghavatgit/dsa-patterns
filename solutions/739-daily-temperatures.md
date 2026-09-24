# Problem 739: Daily Temperatures

## Problem Statement
Given an array of integers `temperatures` represents the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `i-th` day to get a warmer temperature. If there is no future day for which this is possible, keep `answer[i] == 0`.

## Monotonic Stack Approach
Iterate through the array while maintaining a monotonic decreasing stack of indices.
When `temperatures[i] > temperatures[st.top()]`:
- The warmer day for `prev = st.top()` is `i`.
- `answer[prev] = i - prev`.
- Pop `prev` and repeat until invariant is restored.

## Complexity
- Time: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <stack>

std::vector<int> dailyTemperatures(const std::vector<int>& temperatures) {
    int n = temperatures.size();
    std::vector<int> answer(n, 0);
    std::stack<int> st;

    for (int i = 0; i < n; ++i) {
        while (!st.empty() && temperatures[i] > temperatures[st.top()]) {
            int prev_idx = st.top();
            st.pop();
            answer[prev_idx] = i - prev_idx;
        }
        st.push(i);
    }
    return answer;
}
```
