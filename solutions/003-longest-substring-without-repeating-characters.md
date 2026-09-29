# 3. Longest Substring Without Repeating Characters

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(min(m, n)) for index map

## Rust Implementation
```rust
use std::collections::HashMap;

pub fn length_of_longest_substring(s: String) -> i32 {
    let mut char_map = HashMap::new();
    let mut max_len = 0;
    let mut start = 0;

    for (idx, c) in s.chars().enumerate() {
        if let Some(&prev_idx) = char_map.get(&c) {
            if prev_idx >= start {
                start = prev_idx + 1;
            }
        }
        char_map.insert(c, idx);
        max_len = max_len.max(idx - start + 1);
    }
    max_len as i32
}
```
