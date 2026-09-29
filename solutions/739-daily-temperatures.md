# 739. Daily Temperatures

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn daily_temperatures(temperatures: Vec<i32>) -> Vec<i32> {
    let n = temperatures.len();
    let mut res = vec![0; n];
    let mut stack: Vec<usize> = Vec::new();

    for i in 0..n {
        while let Some(&top) = stack.last() {
            if temperatures[i] > temperatures[top] {
                stack.pop();
                res[top] = (i - top) as i32;
            } else {
                break;
            }
        }
        stack.push(i);
    }
    res
}
```
