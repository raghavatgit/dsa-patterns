# Problem 041: First Missing Positive

## Problem Statement
Given an unsorted integer array `nums`. Return the smallest positive integer that is not present in `nums`. You must implement an algorithm that runs in $O(n)$ time and uses $O(1)$ auxiliary space.

## In-Place Cyclic Sort
For each index $i$, place `nums[i]` at its target bucket `nums[i] - 1` while `nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]`.
Scan array: first index where `nums[i] != i + 1` identifies answer $i + 1$.

## Complexity
- Time: $O(N)$
- Space: $O(1)$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>

int firstMissingPositive(std::vector<int>& nums) {
    int n = nums.size();
    for (int i = 0; i < n; ++i) {
        while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
            std::swap(nums[i], nums[nums[i] - 1]);
        }
    }

    for (int i = 0; i < n; ++i) {
        if (nums[i] != i + 1) {
            return i + 1;
        }
    }
    return n + 1;
}
```
