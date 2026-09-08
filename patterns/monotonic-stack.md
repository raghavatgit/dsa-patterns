# Monotonic Stack Pattern

## Concept
A stack that maintains elements in either strictly ascending or strictly descending order. Used to find the Next Greater Element, Next Smaller Element, or solve range maximum problems in linear O(N) time instead of quadratic O(N^2) searches.

## TypeScript Implementation

```typescript
export function dailyTemperatures(temperatures: number[]): number[] {
  const n = temperatures.length;
  const result: number[] = new Array(n).fill(0);
  const stack: number[] = []; // Stores indices

  for (let i = 0; i < n; i++) {
    while (stack.length > 0 && temperatures[i] > temperatures[stack[stack.length - 1]]) {
      const prevIndex = stack.pop()!;
      result[prevIndex] = i - prevIndex;
    }
    stack.push(i);
  }

  return result;
}
```

## Rust Implementation

```rust
pub fn next_greater_element(nums: &[i32]) -> Vec<i32> {
    let n = nums.len();
    let mut result = vec![-1; n];
    let mut stack: Vec<usize> = Vec::with_capacity(n); // Stores indices

    for (i, &val) in nums.iter().enumerate() {
        while let Some(&last_idx) = stack.last() {
            if val > nums[last_idx] {
                result[last_idx] = val;
                stack.pop();
            } else {
                break;
            }
        }
        stack.push(i);
    }

    result
}
```

## Complexity Analysis
* **Time Complexity:** O(N) because each index is pushed and popped at most once.
* **Space Complexity:** O(N) worst-case storage for monotonic tracking.
