# 071. Simplify Path

## Problem Statement
Given an absolute path for a Unix-style file system, convert it to the simplified canonical path.

---

## Stack Transformation
Split input string by `/`. Discard empty tokens and `.`. When token is `..`, pop the top directory from stack if non-empty. Join remaining tokens with `/`.

---

## TypeScript Implementation

```typescript
export function simplifyPath(path: string): string {
  const stack: string[] = [];
  const tokens = path.split('/');

  for (const token of tokens) {
    if (token === '' || token === '.') continue;
    if (token === '..') {
      if (stack.length > 0) stack.pop();
    } else {
      stack.push(token);
    }
  }

  return '/' + stack.join('/');
}
```

---

## Rust Implementation

```rust
pub fn simplify_path(path: String) -> String {
    let mut stack: Vec<&str> = Vec::new();

    for token in path.split('/') {
        match token {
            "" | "." => continue,
            ".." => {
                stack.pop();
            }
            dir => {
                stack.push(dir);
            }
        }
    }

    format!("/{}", stack.join("/"))
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) where N is path character length.
* **Space Complexity:** O(N) stack storage.
