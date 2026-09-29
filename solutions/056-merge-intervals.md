# 56. Merge Intervals

## Complexity
- Time Complexity: O(n log n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn merge(mut intervals: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
    intervals.sort_unstable_by_key(|i| i[0]);
    let mut merged: Vec<Vec<i32>> = Vec::new();

    for interval in intervals {
        if let Some(last) = merged.last_mut() {
            if interval[0] <= last[1] {
                last[1] = std::cmp::max(last[1], interval[1]);
                continue;
            }
        }
        merged.push(interval);
    }

    merged
}
```
