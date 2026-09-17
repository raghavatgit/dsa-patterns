# Problem: Longest Substring Without Repeating Characters

## Problem Statement
Given a string `s`, find the length of the longest substring without duplicate characters.

## Intuition & Approach
Use a dynamic sliding window with two pointers `left` and `right`:
* Maintain a hash map or 128-element lookup array storing the most recent index where each character was observed.
* When character `s[right]` was previously seen at `prev_index >= left`, jump `left = prev_index + 1`.
* Track `max_length = max(max_length, right - left + 1)`.

## TypeScript Implementation

```typescript
export function lengthOfLongestSubstring(s: string): number {
  const lastSeen = new Map<string, number>();
  let maxLength = 0;
  let left = 0;

  for (let right = 0; right < s.length; right++) {
    const char = s[right];
    if (lastSeen.has(char) && lastSeen.get(char)! >= left) {
      left = lastSeen.get(char)! + 1;
    }

    lastSeen.set(char, right);
    maxLength = Math.max(maxLength, right - left + 1);
  }

  return maxLength;
}
```

## Rust Implementation

```rust
use std::collections::HashMap;

pub fn length_of_longest_substring(s: &str) -> i32 {
    let mut last_seen = HashMap::new();
    let mut max_len = 0;
    let mut left = 0;

    for (right, ch) in s.chars().enumerate() {
        if let Some(&prev_idx) = last_seen.get(&ch) {
            if prev_idx >= left {
                left = prev_idx + 1;
            }
        }

        last_seen.insert(ch, right);
        max_len = max_len.max(right - left + 1);
    }

    max_len as i32
}
```

## Complexity Analysis
* **Time Complexity:** O(N) single-pass iteration with O(1) hash map operations.
* **Space Complexity:** O(min(N, ALPHA)) auxiliary space for the character position table.
