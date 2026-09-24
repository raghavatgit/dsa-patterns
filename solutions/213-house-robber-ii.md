# Problem 213: House Robber II

## Problem Statement
You are a professional robber planning to rob houses along a street, but all houses at this place are arranged in a circle.

## Strategy
Houses $0$ and $N - 1$ are adjacent:
- Case 1: Rob from index $0$ to $N - 2$.
- Case 2: Rob from index $1$ to $N - 1$.
Answer is $\max(\text{Case 1}, \text{Case 2})$.

## Complexity
- Time: $O(N)$
- Space: $O(1)$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>

int robLinear(const std::vector<int>& nums, int start, int end) {
    int prev2 = 0, prev1 = 0;
    for (int i = start; i <= end; ++i) {
        int curr = std::max(prev1, prev2 + nums[i]);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}

int rob(const std::vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return 0;
    if (n == 1) return nums[0];

    return std::max(robLinear(nums, 0, n - 2), robLinear(nums, 1, n - 1));
}
```
