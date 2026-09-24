# Problem 072: Edit Distance

## Problem Statement
Given two strings `word1` and `word2`, return the minimum number of operations required to convert `word1` to `word2`. Permitted operations: Insert, Delete, Replace.

## Recurrence
$$dp[i][j] = \begin{cases} dp[i - 1][j - 1] & \text{if } word1[i - 1] == word2[j - 1] \\ 1 + \min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) & \text{otherwise} \end{cases}$$

## Complexity
- Time: $O(M \times N)$
- Space: $O(N)$ with row rolling.

## C++ Implementation
```cpp
#include <string>
#include <vector>
#include <algorithm>

int minDistance(const std::string& word1, const std::string& word2) {
    int m = word1.length(), n = word2.length();
    std::vector<int> dp(n + 1);

    for (int j = 0; j <= n; ++j) dp[j] = j;

    for (int i = 1; i <= m; ++i) {
        int prev = dp[0];
        dp[0] = i;
        for (int j = 1; j <= n; ++j) {
            int temp = dp[j];
            if (word1[i - 1] == word2[j - 1]) {
                dp[j] = prev;
            } else {
                dp[j] = 1 + std::min({dp[j], dp[j - 1], prev});
            }
            prev = temp;
        }
    }
    return dp[n];
}
```
