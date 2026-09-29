# 409. Longest Palindrome

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn longest_palindrome(s: String) -> i32 {
    let mut counts = [0i32; 128];
    for b in s.bytes() {
        counts[b as usize] += 1;
    }
    let mut length = 0;
    let mut has_odd = false;
    for &c in &counts {
        length += (c / 2) * 2;
        if c % 2 == 1 {
            has_odd = true;
        }
    }
    if has_odd { length + 1 } else { length }
}
```

## TypeScript Implementation
```typescript
export function longestPalindrome(s: string): number {
    const counts = new Map<string, number>();
    for (const c of s) {
        counts.set(c, (counts.get(c) || 0) + 1);
    }
    let length = 0;
    let hasOdd = false;
    for (const count of counts.values()) {
        length += Math.floor(count / 2) * 2;
        if (count % 2 === 1) hasOdd = true;
    }
    return hasOdd ? length + 1 : length;
}
```
