# Problem 084: Largest Rectangle in Histogram

## Problem Statement
Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return the area of the largest rectangle in the histogram.

## Monotonic Stack Approach
A bar can be extended as a rectangle height as long as neighboring bars are $\ge$ its height.
Maintain a strictly increasing stack of indices.
When encountering a smaller bar, pop the stack top `h`:
- Height of popped bar: `heights[h]`
- Right boundary: current index `i`
- Left boundary: new stack top (or `-1` if stack empty)
- Width: `i - stack.top() - 1`

## Complexity
- Time: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <stack>
#include <algorithm>

int largestRectangleArea(std::vector<int>& heights) {
    std::stack<int> st;
    heights.push_back(0); // Sentinel to flush remaining stack
    int max_area = 0;

    for (int i = 0; i < static_cast<int>(heights.size()); ++i) {
        while (!st.empty() && heights[st.top()] > heights[i]) {
            int h = heights[st.top()];
            st.pop();
            int width = st.empty() ? i : i - st.top() - 1;
            max_area = std::max(max_area, h * width);
        }
        st.push(i);
    }
    heights.pop_back();
    return max_area;
}
```
