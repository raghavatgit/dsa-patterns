# 125. Valid Palindrome

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn is_palindrome(s: String) -> bool {
    let bytes = s.as_bytes();
    let mut l = 0;
    let mut r = bytes.len().saturating_sub(1);

    while l < r {
        if !bytes[l].is_ascii_alphanumeric() { l += 1; }
        else if !bytes[r].is_ascii_alphanumeric() { r = r.saturating_sub(1); }
        else {
            if bytes[l].to_ascii_lowercase() != bytes[r].to_ascii_lowercase() {
                return false;
            }
            l += 1;
            r = r.saturating_sub(1);
        }
    }
    true
}
```
