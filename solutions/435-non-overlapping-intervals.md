# 435. Non-overlapping Intervals

## Complexity
- Time Complexity: O(n log n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn erase_overlap_intervals(mut intervals: Vec<Vec<i32>>) -> i32 {
    intervals.sort_unstable_by_key(|x| x[1]);
    let mut removals = 0;
    let mut prev_end = i32::MIN;

    for interval in intervals {
        if interval[0] >= prev_end {
            prev_end = interval[1];
        } else {
            removals += 1;
        }
    }
    removals
}
```
