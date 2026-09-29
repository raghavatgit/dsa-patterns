# 76. Minimum Window Substring

## Complexity
- Time Complexity: O(s + t)
- Space Complexity: O(s + t)

## Rust Implementation
```rust
use std::collections::HashMap;

pub fn min_window(s: String, t: String) -> String {
    if t.is_empty() || s.len() < t.len() { return "".to_string(); }
    let mut count_t = HashMap::new();
    for c in t.chars() { *count_t.entry(c).or_insert(0) += 1; }

    let mut window = HashMap::new();
    let mut have = 0;
    let need = count_t.len();
    let s_chars: Vec<char> = s.chars().collect();
    let mut res = (-1, -1);
    let mut res_len = usize::MAX;
    let mut left = 0;

    for right in 0..s_chars.len() {
        let c = s_chars[right];
        *window.entry(c).or_insert(0) += 1;

        if count_t.contains_key(&c) && window[&c] == count_t[&c] {
            have += 1;
        }

        while have == need {
            if (right - left + 1) < res_len {
                res = (left as i32, right as i32);
                res_len = right - left + 1;
            }
            let left_char = s_chars[left];
            *window.get_mut(&left_char).unwrap() -= 1;
            if count_t.contains_key(&left_char) && window[&left_char] < count_t[&left_char] {
                have -= 1;
            }
            left += 1;
        }
    }

    if res.0 == -1 { "".to_string() } else { s_chars[res.0 as usize..=res.1 as usize].iter().collect() }
}
```
