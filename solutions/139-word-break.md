# Problem 139: Word Break

## Problem Statement
Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

## Approach
`dp[i] = true` if `s[0...i - 1]` can be segmented.
For each index `i` from `1` to `N`, and each `j < i`:
If `dp[j] && wordDict.contains(s[j...i - 1])`, set `dp[i] = true` and break.

## Complexity
- Time: $O(N^2 \times L)$ where $L$ is max word length.
- Space: $O(N + \text{dict})$

## C++ Implementation
```cpp
#include <string>
#include <vector>
#include <unordered_set>

bool wordBreak(const std::string& s, const std::vector<std::string>& wordDict) {
    std::unordered_set<std::string> dict(wordDict.begin(), wordDict.end());
    int n = s.length();
    std::vector<bool> dp(n + 1, false);
    dp[0] = true;

    for (int i = 1; i <= n; ++i) {
        for (int j = 0; j < i; ++j) {
            if (dp[j] && dict.count(s.substr(j, i - j))) {
                dp[i] = true;
                break;
            }
        }
    }
    return dp[n];
}
```
