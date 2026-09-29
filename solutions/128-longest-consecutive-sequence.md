# 128. Longest Consecutive Sequence

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::collections::HashSet;

pub fn longest_consecutive(nums: Vec<i32>) -> i32 {
    let set: HashSet<i32> = nums.into_iter().collect();
    let mut max_streak = 0;

    for &x in &set {
        if !set.contains(&(x - 1)) {
            let mut curr = x;
            let mut streak = 1;
            while set.contains(&(curr + 1)) {
                curr += 1;
                streak += 1;
            }
            max_streak = max_streak.max(streak);
        }
    }
    max_streak
}
```
