# 42. Trapping Rain Water

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn trap(height: Vec<i32>) -> i32 {
    let mut left = 0;
    let mut right = height.len() - 1;
    let mut max_l = 0;
    let mut max_r = 0;
    let mut water = 0;

    while left < right {
        if height[left] <= height[right] {
            if height[left] >= max_l {
                max_l = height[left];
            } else {
                water += max_l - height[left];
            }
            left += 1;
        } else {
            if height[right] >= max_r {
                max_r = height[right];
            } else {
                water += max_r - height[right];
            }
            right -= 1;
        }
    }
    water
}
```
