# 125. Valid Palindrome

## Problem Statement
Given a string `s`, return `true` if it is a palindrome considering only alphanumeric characters and ignoring cases.

---

## TypeScript Implementation

```typescript
export function isPalindrome(s: string): boolean {
  let left = 0;
  let right = s.length - 1;

  function isAlphanumeric(code: number): boolean {
    return (code >= 48 && code <= 57) || // 0-9
           (code >= 65 && code <= 90) || // A-Z
           (code >= 97 && code <= 122);  // a-z
  }

  while (left < right) {
    while (left < right && !isAlphanumeric(s.charCodeAt(left))) left++;
    while (left < right && !isAlphanumeric(s.charCodeAt(right))) right--;

    if (s[left].toLowerCase() !== s[right].toLowerCase()) {
      return false;
    }
    left++;
    right--;
  }

  return true;
}
```

---

## Rust Implementation

```rust
pub fn is_palindrome(s: String) -> bool {
    let bytes = s.as_bytes();
    let mut left = 0;
    let mut right = bytes.len().saturating_sub(1);

    while left < right {
        while left < right && !bytes[left].is_ascii_alphanumeric() {
            left += 1;
        }
        while left < right && !bytes[right].is_ascii_alphanumeric() {
            right -= 1;
        }

        if bytes[left].to_ascii_lowercase() != bytes[right].to_ascii_lowercase() {
            return false;
        }
        left += 1;
        if right > 0 { right -= 1; }
    }

    true
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) two pointers.
* **Space Complexity:** O(1) in-place validation.
