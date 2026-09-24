# Problem 424: Longest Repeating Character Replacement

## Problem Statement
You are given a string `s` consisting of uppercase English letters and an integer `k`. You can choose any character of the string and change it to any other uppercase English letter up to `k` times. Return the length of the longest substring containing the same letter you can get after performing the above operations.

## Key Invariant
Window length is valid if:
$$\text{window\_length} - \max(\text{count}) \le k$$
We track `max_count` within the window. If condition fails, we shrink `left` by 1.

## Complexity
- Time: $O(N)$
- Space: $O(1)$ (26 uppercase letters)

## C++ Implementation
```cpp
#include <string>
#include <vector>
#include <algorithm>

int characterReplacement(const std::string& s, int k) {
    std::vector<int> count(26, 0);
    int max_count = 0;
    int left = 0;
    int max_len = 0;

    for (int right = 0; right < static_cast<int>(s.length()); ++right) {
        int idx = s[right] - 'A';
        count[idx]++;
        max_count = std::max(max_count, count[idx]);

        while ((right - left + 1) - max_count > k) {
            count[s[left] - 'A']--;
            left++;
        }

        max_len = std::max(max_len, right - left + 1);
    }
    return max_len;
}
```
