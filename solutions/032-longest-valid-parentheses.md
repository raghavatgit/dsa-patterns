# Problem 032: Longest Valid Parentheses

## Problem Statement
Given a string containing just the characters `'('` and `')'`, return the length of the longest valid (well-forming) parentheses substring.

## Dual-Pass Two-Pointer
- Left-to-right pass: Track `left` and `right`. If `left == right`, record $2 \times right$. If `right > left`, reset both to 0.
- Right-to-left pass: Same logic symmetric for excess `'('`.

## Complexity
- Time: $O(N)$
- Space: $O(1)$

## C++ Implementation
```cpp
#include <string>
#include <algorithm>

int longestValidParentheses(const std::string& s) {
    int left = 0, right = 0, max_len = 0;
    int n = s.length();

    for (int i = 0; i < n; ++i) {
        if (s[i] == '(') left++;
        else right++;

        if (left == right) max_len = std::max(max_len, 2 * right);
        else if (right > left) left = right = 0;
    }

    left = right = 0;
    for (int i = n - 1; i >= 0; --i) {
        if (s[i] == '(') left++;
        else right++;

        if (left == right) max_len = std::max(max_len, 2 * left);
        else if (left > right) left = right = 0;
    }

    return max_len;
}
```
