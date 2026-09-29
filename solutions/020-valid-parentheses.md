# 20. Valid Parentheses

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn is_valid(s: String) -> bool {
    let mut stack = Vec::new();
    for c in s.chars() {
        match c {
            '(' => stack.push(')'),
            '{' => stack.push('}'),
            '[' => stack.push(']'),
            ')' | '}' | ']' => {
                if stack.pop() != Some(c) {
                    return false;
                }
            }
            _ => return false,
        }
    }
    stack.is_empty()
}
```

## TypeScript Implementation
```typescript
export function isValid(s: string): boolean {
    const stack: string[] = [];
    const map: Record<string, string> = { ')': '(', '}': '{', ']': '[' };

    for (const char of s) {
        if (char === '(' || char === '{' || char === '[') {
            stack.push(char);
        } else if (map[char]) {
            if (stack.pop() !== map[char]) return false;
        }
    }

    return stack.length === 0;
}
```
