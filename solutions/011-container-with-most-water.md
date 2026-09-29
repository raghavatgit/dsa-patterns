# 11. Container With Most Water

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn max_area(height: Vec<i32>) -> i32 {
    let mut left = 0;
    let mut right = height.len() - 1;
    let mut max_water = 0;

    while left < right {
        let w = (right - left) as i32;
        let h = height[left].min(height[right]);
        max_water = max_water.max(w * h);

        if height[left] < height[right] {
            left += 1;
        } else {
            right -= 1;
        }
    }
    max_water
}
```
