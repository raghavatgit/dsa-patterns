# Problem: Container With Most Water

## Problem Statement
You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i`-th line are `(i, 0)` and `(i, height[i])`. Find two lines that together with the x-axis form a container, such that the container contains the most water. Return the maximum amount of water a container can store.

## Intuition & Approach
Two-Pointer Inwards Contraction:
1. Initialize `left = 0` and `right = n - 1`.
2. Area is bounded by the shorter line: `area = min(height[left], height[right]) * (right - left)`.
3. Moving the taller line inwards can only decrease the width while the height remains bounded by the shorter line (cannot increase area).
4. Therefore, greedily advance the pointer pointing to the shorter vertical bar.
5. Time Complexity: $O(N)$ visiting each line once. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function maxArea(height: number[]): number {
  let left = 0;
  let right = height.length - 1;
  let maxWater = 0;

  while (left < right) {
    const width = right - left;
    const h = Math.min(height[left], height[right]);
    maxWater = Math.max(maxWater, width * h);

    if (height[left] < height[right]) {
      left++;
    } else {
      right--;
    }
  }

  return maxWater;
}
```

## Rust Implementation

```rust
pub fn max_area(height: Vec<i32>) -> i32 {
    let mut left = 0;
    let mut right = height.len() - 1;
    let mut max_water = 0;

    while left < right {
        let width = (right - left) as i32;
        let h = height[left].min(height[right]);
        max_water = max_water.max(width * h);

        if height[left] < height[right] {
            left += 1;
        } else {
            right -= 1;
        }
    }

    max_water
}
```
