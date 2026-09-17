# Problem: Largest Rectangle in Histogram

## Problem Statement
Given an array of integers `heights` representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

## Intuition & Approach
Using a Monotonic Increasing Stack:
1. Maintain indices of bars whose heights are in non-decreasing order.
2. When current bar `heights[i]` is smaller than the bar at stack top, pop the top index `curr`.
3. The height of the rectangle formed with `heights[curr]` is `heights[curr]`.
4. The width extends between the current index `i` (right boundary, exclusive) and the new stack top (left boundary, exclusive): `width = i - stack.top() - 1` (or `i` if stack is empty).
5. Append a virtual bar of height 0 at the end to flush all remaining elements from the stack.
6. Time Complexity: $O(N)$ since each bar is pushed and popped at most once. Space Complexity: $O(N)$ stack memory.

## TypeScript Implementation

```typescript
export function largestRectangleArea(heights: number[]): number {
  const stack: number[] = [];
  let maxArea = 0;
  const n = heights.length;

  for (let i = 0; i <= n; i++) {
    const currentHeight = i === n ? 0 : heights[i];

    while (stack.length > 0 && currentHeight < heights[stack[stack.length - 1]]) {
      const h = heights[stack.pop()!];
      const w = stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
      maxArea = Math.max(maxArea, h * w);
    }

    stack.push(i);
  }

  return maxArea;
}
```

## Rust Implementation

```rust
pub fn largest_rectangle_area(heights: Vec<i32>) -> i32 {
    let mut stack: Vec<usize> = Vec::new();
    let mut max_area = 0;
    let n = heights.len();

    for i in 0..=n {
        let curr_h = if i == n { 0 } else { heights[i] };

        while let Some(&top_idx) = stack.last() {
            if curr_h < heights[top_idx] {
                stack.pop();
                let h = heights[top_idx];
                let w = if stack.is_empty() {
                    i as i32
                } else {
                    (i - stack.last().unwrap() - 1) as i32
                };
                max_area = max_area.max(h * w);
            } else {
                break;
            }
        }

        stack.push(i);
    }

    max_area
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_histogram_basic() {
        assert_eq!(largest_rectangle_area(vec![2, 1, 5, 6, 2, 3]), 10);
        assert_eq!(largest_rectangle_area(vec![2, 4]), 4);
    }
}
```
