# Problem 042: Trapping Rain Water

## Problem Statement
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

## Two-Pointer Approach
Water trapped at position `i` is determined by $\min(\text{max\_left}, \text{max\_right}) - height[i]$.
By comparing `left_max` and `right_max`, the side with the smaller max bound is the bottleneck and can be resolved immediately without knowing the exact shape on the other side.

## Complexity
- Time Complexity: $O(N)$
- Space Complexity: $O(1)$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>

int trap(const std::vector<int>& height) {
    if (height.empty()) return 0;

    int left = 0, right = static_cast<int>(height.size()) - 1;
    int left_max = 0, right_max = 0;
    int total_water = 0;

    while (left < right) {
        if (height[left] <= height[right]) {
            if (height[left] >= left_max) {
                left_max = height[left];
            } else {
                total_water += left_max - height[left];
            }
            ++left;
        } else {
            if (height[right] >= right_max) {
                right_max = height[right];
            } else {
                total_water += right_max - height[right];
            }
            --right;
        }
    }
    return total_water;
}
```
