# 84. Largest Rectangle in Histogram

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn largest_rectangle_area(heights: Vec<i32>) -> i32 {
    let mut stack: Vec<usize> = Vec::new();
    let mut max_area = 0;
    let n = heights.len();

    for i in 0..=n {
        let h = if i == n { 0 } else { heights[i] };
        while let Some(&top) = stack.last() {
            if h < heights[top] {
                stack.pop();
                let height = heights[top];
                let width = match stack.last() {
                    Some(&prev) => (i - prev - 1) as i32,
                    None => i as i32,
                };
                max_area = std::cmp::max(max_area, height * width);
            } else {
                break;
            }
        }
        stack.push(i);
    }

    max_area
}
```
