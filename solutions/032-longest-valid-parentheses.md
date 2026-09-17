# Problem: Longest Valid Parentheses

## Problem Statement
Given a string containing just the characters `'('` and `')'`, return the length of the longest valid (well-formed) parentheses substring.

## Intuition & Approach
Two-Pass Counter ($O(1)$ Space Optimization):
1. **Left-to-Right Pass**: Maintain counts of `left` and `right` parentheses.
   - When `left == right`, update `max_len = max(max_len, 2 * right)`.
   - If `right > left`, invalid substring reached; reset both `left = 0` and `right = 0`.
2. **Right-to-Left Pass**: Catches scenarios where `left > right` throughout (e.g. `"(()"`):
   - When `left == right`, update `max_len = max(max_len, 2 * left)`.
   - If `left > right`, reset both counters to 0.
3. Time Complexity: $O(N)$ with two linear scans. Space Complexity: $O(1)$ auxiliary variables.

## TypeScript Implementation

```typescript
export function longestValidParentheses(s: string): number {
  let left = 0;
  let right = 0;
  let maxLen = 0;

  // Left to right scan
  for (let i = 0; i < s.length; i++) {
    if (s[i] === '(') left++;
    else right++;

    if (left === right) {
      maxLen = Math.max(maxLen, 2 * right);
    } else if (right > left) {
      left = 0;
      right = 0;
    }
  }

  left = 0;
  right = 0;

  // Right to left scan
  for (let i = s.length - 1; i >= 0; i--) {
    if (s[i] === '(') left++;
    else right++;

    if (left === right) {
      maxLen = Math.max(maxLen, 2 * left);
    } else if (left > right) {
      left = 0;
      right = 0;
    }
  }

  return maxLen;
}
```

## Rust Implementation

```rust
pub fn longest_valid_parentheses(s: String) -> i32 {
    let chars: Vec<char> = s.chars().collect();
    let n = chars.len();
    let mut max_len = 0;

    let mut left = 0;
    let mut right = 0;
    for &c in &chars {
        if c == '(' { left += 1; } else { right += 1; }

        if left == right {
            max_len = max_len.max(2 * right);
        } else if right > left {
            left = 0;
            right = 0;
        }
    }

    left = 0;
    right = 0;
    for &c in chars.iter().rev() {
        if c == '(' { left += 1; } else { right += 1; }

        if left == right {
            max_len = max_len.max(2 * left);
        } else if left > right {
            left = 0;
            right = 0;
        }
    }

    max_len
}
```
