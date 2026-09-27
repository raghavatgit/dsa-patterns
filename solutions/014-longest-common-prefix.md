# 014. Longest Common Prefix

## Problem Statement
Write a function to find the longest common prefix string amongst an array of strings. If there is no common prefix, return an empty string `""`.

---

## TypeScript Implementation

```typescript
export function longestCommonPrefix(strs: string[]): string {
  if (strs.length === 0) return "";
  let prefix = strs[0];

  for (let i = 1; i < strs.length; i++) {
    while (strs[i].indexOf(prefix) !== 0) {
      prefix = prefix.substring(0, prefix.length - 1);
      if (prefix === "") return "";
    }
  }

  return prefix;
}
```

---

## Rust Implementation

```rust
pub fn longest_common_prefix(strs: Vec<String>) -> String {
    if strs.is_empty() {
        return String::new();
    }

    let mut prefix = strs[0].as_str();

    for s in strs.iter().skip(1) {
        while !s.starts_with(prefix) {
            if prefix.is_empty() {
                return String::new();
            }
            prefix = &prefix[..prefix.len() - 1];
        }
    }

    prefix.to_string()
}
```

---

## Complexity Analysis
* **Time Complexity:** O(S) where S is the sum of characters across all strings.
* **Space Complexity:** O(1) auxiliary space.
