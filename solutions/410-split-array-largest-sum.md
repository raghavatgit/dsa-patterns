# Problem 410: Split Array Largest Sum

## Problem Statement
Given an integer array `nums` and an integer `k`, split `nums` into `k` non-empty subarrays such that the largest sum of any subarray is minimized. Return the minimized largest sum.

## Monotonic Binary Search on Answer
- Lower bound: $\max(nums)$
- Upper bound: $\sum nums$
Predicate `canSplit(max_sum)`: greedily pack elements into subarrays without exceeding `max_sum`. If required subarrays $\le k$, condition is satisfiable.

## Complexity
- Time: $O(N \log(\sum nums))$
- Space: $O(1)$

## C++ Implementation
```cpp
#include <vector>
#include <numeric>
#include <algorithm>

class Solution {
    bool canSplit(const std::vector<int>& nums, int k, long long max_sum) {
        int count = 1;
        long long current_sum = 0;

        for (int num : nums) {
            if (current_sum + num > max_sum) {
                count++;
                current_sum = num;
                if (count > k) return false;
            } else {
                current_sum += num;
            }
        }
        return true;
    }

public:
    int splitArray(const std::vector<int>& nums, int k) {
        long long low = *std::max_element(nums.begin(), nums.end());
        long long high = std::accumulate(nums.begin(), nums.end(), 0LL);
        long long ans = high;

        while (low <= high) {
            long long mid = low + (high - low) / 2;
            if (canSplit(nums, k, mid)) {
                ans = mid;
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return static_cast<int>(ans);
    }
};
```
