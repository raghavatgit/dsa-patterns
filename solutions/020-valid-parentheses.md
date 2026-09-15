# Problem: Valid Parentheses

## Problem Statement
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.
An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

## Intuition & Approach
Use a LIFO Stack:
* When an opening bracket is encountered, push it onto the stack.
* When a closing bracket is encountered, verify that the stack is non-empty and the top element matches the closing bracket type.
* After iterating through the string, the stack must be empty for the string to be valid.

## TypeScript Implementation

```typescript
export function isValid(s: string): boolean {
  if (s.length % 2 !== 0) return false;

  const stack: string[] = [];
  const map: Record<string, string> = {
    ')': '(',
    '}': '{',
    ']': '['
  };

  for (const char of s) {
    if (char === '(' || char === '{' || char === '[') {
      stack.push(char);
    } else {
      if (stack.length === 0 || stack.pop() !== map[char]) {
        return false;
      }
    }
  }

  return stack.length === 0;
}
```

## Rust Implementation

```rust
pub fn is_valid(s: &str) -> bool {
    if s.len() % 2 != 0 {
        return false;
    }

    let mut stack = Vec::with_capacity(s.len());

    for ch in s.chars() {
        match ch {
            '(' | '{' | '[' => stack.push(ch),
            ')' => if stack.pop() != Some('(') { return false; },
            '}' => if stack.pop() != Some('{') { return false; },
            ']' => if stack.pop() != Some('[') { return false; },
            _ => return false,
        }
    }

    stack.is_empty()
}
```

## Complexity Analysis
* **Time Complexity:** O(N) single-pass linear scan.
* **Space Complexity:** O(N) stack memory in the worst case (all open brackets).
