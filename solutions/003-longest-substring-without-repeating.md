# Problem 003: Longest Substring Without Repeating Characters

## Problem Statement
Given a string `s`, find the length of the longest substring without repeating characters.

## Approach
Sliding window with last-seen character indices.
When character `s[right]` is encountered at index `last_seen[s[right]] >= left`, shift `left` forward to `last_seen[s[right]] + 1`.
Update `max_len = max(max_len, right - left + 1)`.

## Complexity
- Time Complexity: $O(N)$
- Space Complexity: $O(\min(N, \Sigma))$ where $\Sigma$ is the alphabet size (128 for ASCII).

## C++ Implementation
```cpp
#include <string>
#include <vector>
#include <algorithm>

int lengthOfLongestSubstring(const std::string& s) {
    std::vector<int> last_pos(128, -1);
    int max_len = 0;
    int left = 0;

    for (int right = 0; right < static_cast<int>(s.length()); ++right) {
        unsigned char c = static_cast<unsigned char>(s[right]);
        if (last_pos[c] >= left) {
            left = last_pos[c] + 1;
        }
        last_pos[c] = right;
        max_len = std::max(max_len, right - left + 1);
    }
    return max_len;
}
```
