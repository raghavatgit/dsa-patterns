# Problem 300: Longest Increasing Subsequence

## Problem Statement
Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

## Patience Sorting Algorithm
Maintain `tails` array where `tails[i]` stores the smallest tail of all increasing subsequences of length `i + 1`.
For each `x` in `nums`:
- Binary search `std::lower_bound` for first element $\ge x$.
- If found, update `tails[idx] = x`.
- If not found, append `x` to `tails`.
Length of `tails` at completion is the length of the LIS.

## Complexity
- Time: $O(N \log N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>

int lengthOfLIS(const std::vector<int>& nums) {
    std::vector<int> tails;
    for (int x : nums) {
        auto it = std::lower_bound(tails.begin(), tails.end(), x);
        if (it == tails.end()) {
            tails.push_back(x);
        } else {
            *it = x;
        }
    }
    return static_cast<int>(tails.size());
}
```
