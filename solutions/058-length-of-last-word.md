# 058. Length of Last Word

## Problem Statement
Given a string `s` consisting of words and spaces, return the length of the last word in the string.

---

## TypeScript Implementation

```typescript
export function lengthOfLastWord(s: string): number {
  let len = 0;
  let i = s.length - 1;

  while (i >= 0 && s[i] === ' ') i--;
  while (i >= 0 && s[i] !== ' ') {
    len++;
    i--;
  }

  return len;
}
```

---

## Rust Implementation

```rust
pub fn length_of_last_word(s: String) -> i32 {
    s.trim_end().chars().rev().take_while(|c| *c != ' ').count() as i32
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) backward traversal.
* **Space Complexity:** O(1) auxiliary space.
