# Problem 076: Minimum Window Substring

## Problem Statement
Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.

## Approach
1. Build frequency map for `t`. Total distinct characters required = `required`.
2. Expand `right` pointer over `s`. Decrement deficit for `s[right]`. When a character frequency matches `t`, increment `formed`.
3. When `formed == required`, contract window using `left` to minimize length while retaining valid invariant.

## Complexity
- Time: $O(M + N)$
- Space: $O(1)$ fixed alphabet size 128.

## C++ Implementation
```cpp
#include <string>
#include <vector>
#include <climits>

std::string minWindow(const std::string& s, const std::string& t) {
    if (s.empty() || t.empty() || s.length() < t.length()) return "";

    std::vector<int> target_freq(128, 0);
    for (char c : t) target_freq[static_cast<unsigned char>(c)]++;

    int required = 0;
    for (int count : target_freq) {
        if (count > 0) required++;
    }

    std::vector<int> window_freq(128, 0);
    int formed = 0;
    int left = 0, min_len = INT_MAX, start_idx = 0;

    for (int right = 0; right < static_cast<int>(s.length()); ++right) {
        unsigned char c = static_cast<unsigned char>(s[right]);
        window_freq[c]++;
        if (target_freq[c] > 0 && window_freq[c] == target_freq[c]) {
            formed++;
        }

        while (left <= right && formed == required) {
            if (right - left + 1 < min_len) {
                min_len = right - left + 1;
                start_idx = left;
            }

            unsigned char left_char = static_cast<unsigned char>(s[left]);
            window_freq[left_char]--;
            if (target_freq[left_char] > 0 && window_freq[left_char] < target_freq[left_char]) {
                formed--;
            }
            left++;
        }
    }

    return min_len == INT_MAX ? "" : s.substr(start_idx, min_len);
}
```
