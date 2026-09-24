# Problem 312: Burst Balloons

## Problem Statement
You are given `n` balloons, indexed from `0` to `n - 1`. If you burst the `i-th` balloon, you will get `nums[i - 1] * nums[i] * nums[i + 1]` coins. Return the maximum coins you can collect by bursting balloons wisely.

## Reverse Dynamic Programming
Instead of choosing which balloon to burst first, choose which balloon `k` to burst *last* in the subinterval `(i, j)`:
$$dp[i][j] = \max_{i < k < j}(dp[i][k] + dp[k][j] + nums[i] \times nums[k] \times nums[j])$$

## Complexity
- Time: $O(N^3)$
- Space: $O(N^2)$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>

int maxCoins(std::vector<int>& nums) {
    int n = nums.size();
    std::vector<int> val(n + 2, 1);
    for (int i = 0; i < n; ++i) val[i + 1] = nums[i];

    std::vector<std::vector<int>> dp(n + 2, std::vector<int>(n + 2, 0));

    for (int len = 1; len <= n; ++len) {
        for (int i = 1; i <= n - len + 1; ++i) {
            int j = i + len - 1;
            for (int k = i; k <= j; ++k) {
                dp[i][j] = std::max(dp[i][j],
                    dp[i][k - 1] + dp[k + 1][j] + val[i - 1] * val[k] * val[j + 1]);
            }
        }
    }
    return dp[1][n];
}
```
