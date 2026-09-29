# 127. Word Ladder

## Complexity
- Time Complexity: O(m^2 * n)
- Space Complexity: O(m * n)

## Rust Implementation
```rust
use std::collections::{HashSet, VecDeque};

pub fn ladder_length(begin_word: String, end_word: String, word_list: Vec<String>) -> i32 {
    let mut dict: HashSet<String> = word_list.into_iter().collect();
    if !dict.contains(&end_word) { return 0; }

    let mut queue = VecDeque::new();
    queue.push_back((begin_word, 1));

    while let Some((curr, dist)) = queue.pop_front() {
        if curr == end_word { return dist; }
        let mut chars: Vec<char> = curr.chars().collect();
        for i in 0..chars.len() {
            let orig = chars[i];
            for c in b'a'..=b'z' {
                chars[i] = c as char;
                let candidate: String = chars.iter().collect();
                if dict.remove(&candidate) {
                    queue.push_back((candidate, dist + 1));
                }
            }
            chars[i] = orig;
        }
    }
    0
}
```
