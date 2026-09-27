# 005. Longest Palindromic Substring

## Problem Statement
Given a string `s`, return the longest palindromic substring in `s`.

---

## Expand Around Center Strategy
A palindrome mirrors around its center. In a string of length `n`, there are `2n - 1` possible centers (single character or pair of characters). Expanding around each center takes O(n) time, yielding O(n^2) total time with O(1) space.

---

## TypeScript Implementation

```typescript
export function longestPalindrome(s: string): string {
  if (s.length <= 1) return s;
  let start = 0;
  let maxLen = 1;

  function expand(left: number, right: number) {
    while (left >= 0 && right < s.length && s[left] === s[right]) {
      const len = right - left + 1;
      if (len > maxLen) {
        maxLen = len;
        start = left;
      }
      left--;
      right++;
    }
  }

  for (let i = 0; i < s.length; i++) {
    expand(i, i);     // Odd length
    expand(i, i + 1); // Even length
  }

  return s.substring(start, start + maxLen);
}
```

---

## Rust Implementation

```rust
pub fn longest_palindrome(s: String) -> String {
    let bytes = s.as_bytes();
    if bytes.len() <= 1 {
        return s;
    }

    let mut start = 0;
    let mut max_len = 1;

    for i in 0..bytes.len() {
        // Odd
        let (mut l, mut r) = (i as i32, i as i32);
        while l >= 0 && (r as usize) < bytes.len() && bytes[l as usize] == bytes[r as usize] {
            let len = (r - l + 1) as usize;
            if len > max_len {
                max_len = len;
                start = l as usize;
            }
            l -= 1;
            r += 1;
        }

        // Even
        let (mut l, mut r) = (i as i32, (i + 1) as i32);
        while l >= 0 && (r as usize) < bytes.len() && bytes[l as usize] == bytes[r as usize] {
            let len = (r - l + 1) as usize;
            if len > max_len {
                max_len = len;
                start = l as usize;
            }
            l -= 1;
            r += 1;
        }
    }

    s[start..start + max_len].to_string()
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N^2) worst case.
* **Space Complexity:** O(1) auxiliary space.
