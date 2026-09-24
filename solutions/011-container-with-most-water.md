# Problem 011: Container With Most Water

## Problem Statement
You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i-th` line are `(i, 0)` and `(i, height[i])`. Find two lines that together with the x-axis form a container, such that the container contains the most water. Return the maximum amount of water a container can store.

## Intuition
Start with pointers at both boundaries. The width is maximized. Area is constrained by $\min(height[left], height[right])$. To find a larger area with a smaller width, we must strictly move the pointer pointing to the shorter vertical line inward.

## Complexity
- Time: $O(N)$
- Space: $O(1)$

## C++ Implementation
```cpp
#include <vector>
#include <algorithm>

int maxArea(const std::vector<int>& height) {
    int left = 0;
    int right = static_cast<int>(height.size()) - 1;
    int max_water = 0;

    while (left < right) {
        int h = std::min(height[left], height[right]);
        int width = right - left;
        max_water = std::max(max_water, h * width);

        if (height[left] < height[right]) {
            ++left;
        } else {
            --right;
        }
    }
    return max_water;
}
```

## Rust Implementation
```rust
pub fn max_area(height: Vec<i32>) -> i32 {
    let mut left = 0;
    let mut right = height.len() - 1;
    let mut max_water = 0;

    while left < right {
        let h = height[left].min(height[right]);
        let width = (right - left) as i32;
        max_water = max_water.max(h * width);

        if height[left] < height[right] {
            left += 1;
        } else {
            right -= 1;
        }
    }
    max_water
}
```
