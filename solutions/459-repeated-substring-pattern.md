# 459. Repeated Substring Pattern

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn repeated_substring_pattern(s: String) -> bool {
    let doubled = format!("{}{}", s, s);
    let sub = &doubled[1..doubled.len() - 1];
    sub.contains(&s)
}
```

## TypeScript Implementation
```typescript
export function repeatedSubstringPattern(s: string): boolean {
    const doubled = s + s;
    return doubled.slice(1, -1).includes(s);
}
```
