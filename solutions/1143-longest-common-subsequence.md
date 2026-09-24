# Problem 1143: Longest Common Subsequence

## Problem Statement
Given two strings `text1` and `text2`, return the length of their longest common subsequence. If there is no common subsequence, return `0`.

## Recurrence
$$dp[i][j] = \begin{cases} dp[i - 1][j - 1] + 1 & \text{if } text1[i - 1] == text2[j - 1] \\ \max(dp[i - 1][j], dp[i][j - 1]) & \text{otherwise} \end{cases}$$

## Space Optimized Implementation
Can be reduced to two rows or a single 1D array of size $\min(M, N) + 1$.

## Complexity
- Time: $O(M \times N)$
- Space: $O(\min(M, N))$

## C++ Implementation
```cpp
#include <string>
#include <vector>
#include <algorithm>

int longestCommonSubsequence(const std::string& text1, const std::string& text2) {
    int m = text1.length();
    int n = text2.length();
    if (m < n) return longestCommonSubsequence(text2, text1);

    std::vector<int> prev(n + 1, 0);
    std::vector<int> curr(n + 1, 0);

    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (text1[i - 1] == text2[j - 1]) {
                curr[j] = prev[j - 1] + 1;
            } else {
                curr[j] = std::max(prev[j], curr[j - 1]);
            }
        }
        prev = curr;
    }
    return prev[n];
}
```
