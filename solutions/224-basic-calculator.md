# Problem 224: Basic Calculator

## Problem Statement
Given a string `s` representing a valid expression, implement a basic calculator to evaluate it. Handles `+`, `-`, `(`, `)`, and spaces.

## Complexity
- Time: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <string>
#include <stack>

int calculate(const std::string& s) {
    std::stack<int> st;
    int result = 0;
    int number = 0;
    int sign = 1;

    for (char c : s) {
        if (isdigit(c)) {
            number = 10 * number + (c - '0');
        } else if (c == '+') {
            result += sign * number;
            number = 0;
            sign = 1;
        } else if (c == '-') {
            result += sign * number;
            number = 0;
            sign = -1;
        } else if (c == '(') {
            st.push(result);
            st.push(sign);
            result = 0;
            sign = 1;
        } else if (c == ')') {
            result += sign * number;
            number = 0;
            result *= st.top(); st.pop(); // Multiply by sign
            result += st.top(); st.pop(); // Add previous result
        }
    }
    if (number != 0) result += sign * number;
    return result;
}
```
