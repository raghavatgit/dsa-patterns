# Problem 085: Maximal Rectangle

## Problem Statement
Given a `rows x cols` binary `matrix` filled with `'0'`s and `'1'`s, find the largest rectangle containing only `'1'`s and return its area.

## Approach
Reduce 2D problem into $M$ instances of Problem 084 (Largest Rectangle in Histogram).
Maintain an array `heights` of size $N$. For each row:
- If `matrix[r][c] == '1'`, `heights[c] += 1`
- If `matrix[r][c] == '0'`, `heights[c] = 0`
Run monotonic stack algorithm on `heights`.

## Complexity
- Time: $O(M \times N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <stack>
#include <algorithm>

int maximalRectangle(const std::vector<std::vector<char>>& matrix) {
    if (matrix.empty() || matrix[0].empty()) return 0;
    int rows = matrix.size();
    int cols = matrix[0].size();
    std::vector<int> heights(cols, 0);
    int max_area = 0;

    for (int r = 0; r < rows; ++r) {
        for (int c = 0; c < cols; ++c) {
            heights[c] = (matrix[r][c] == '1') ? heights[c] + 1 : 0;
        }

        std::stack<int> st;
        std::vector<int> h = heights;
        h.push_back(0);
        for (int i = 0; i < static_cast<int>(h.size()); ++i) {
            while (!st.empty() && h[st.top()] > h[i]) {
                int height = h[st.top()];
                st.pop();
                int width = st.empty() ? i : i - st.top() - 1;
                max_area = std::max(max_area, height * width);
            }
            st.push(i);
        }
    }
    return max_area;
}
```
