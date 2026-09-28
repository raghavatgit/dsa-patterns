# 3. Longest Substring Without Repeating Characters

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(min(m, n))

## Rust Implementation
```rust
use std::collections::HashMap;

pub fn length_of_longest_substring(s: String) -> i32 {
    let mut last_seen = HashMap::new();
    let mut max_len = 0;
    let mut start = 0;

    for (i, c) in s.chars().enumerate() {
        if let Some(&prev_idx) = last_seen.get(&c) {
            if prev_idx >= start {
                start = prev_idx + 1;
            }
        }
        last_seen.insert(c, i);
        max_len = std::cmp::max(max_len, i - start + 1);
    }

    max_len as i32
}
```
