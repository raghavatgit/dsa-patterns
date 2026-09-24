# Problem 198: House Robber

## Problem Statement
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

## Recurrence Relation
$$dp[i] = \max(dp[i - 1], dp[i - 2] + nums[i])$$
Since only two previous states are needed, optimize space to $O(1)$.

## Complexity
- Time Complexity: $O(N)$
- Space Complexity: $O(1)$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>

int rob(const std::vector<int>& nums) {
    int prev2 = 0; // dp[i - 2]
    int prev1 = 0; // dp[i - 1]

    for (int num : nums) {
        int current = std::max(prev1, prev2 + num);
        prev2 = prev1;
        prev1 = current;
    }
    return prev1;
}
```
