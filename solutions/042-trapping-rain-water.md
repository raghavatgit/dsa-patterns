# Problem: Trapping Rain Water

## Problem Statement
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

## Intuition & Approach
The water trapped on top of any bar `i` is determined by `min(maxLeft, maxRight) - height[i]`. Using two converging pointers from the outer ends inward:
* If `height[left] < height[right]`: Water level at `left` is strictly bounded by `maxLeft` because a taller barrier exists to its right.
* Update `maxLeft` or accumulate trapped water, then advance `left`.
* Mirror logic for `right`.

## TypeScript Implementation

```typescript
export function trap(height: number[]): number {
  if (height.length === 0) return 0;

  let left = 0;
  let right = height.length - 1;
  let maxLeft = 0;
  let maxRight = 0;
  let totalWater = 0;

  while (left < right) {
    if (height[left] <= height[right]) {
      if (height[left] >= maxLeft) {
        maxLeft = height[left];
      } else {
        totalWater += maxLeft - height[left];
      }
      left++;
    } else {
      if (height[right] >= maxRight) {
        maxRight = height[right];
      } else {
        totalWater += maxRight - height[right];
      }
      right--;
    }
  }

  return totalWater;
}
```

## Rust Implementation

```rust
pub fn trap(height: &[i32]) -> i32 {
    if height.is_empty() {
        return 0;
    }

    let mut left = 0;
    let mut right = height.len() - 1;
    let mut max_left = 0;
    let mut max_right = 0;
    let mut total_water = 0;

    while left < right {
        if height[left] <= height[right] {
            if height[left] >= max_left {
                max_left = height[left];
            } else {
                total_water += max_left - height[left];
            }
            left += 1;
        } else {
            if height[right] >= max_right {
                max_right = height[right];
            } else {
                total_water += max_right - height[right];
            }
            right -= 1;
        }
    }

    total_water
}
```

## Complexity Analysis
* **Time Complexity:** O(N) single pass visiting each bar index once.
* **Space Complexity:** O(1) constant auxiliary space.
