# 387. First Unique Character in a String

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn first_uniq_char(s: String) -> i32 {
    let mut freq = [0i32; 26];
    for b in s.bytes() {
        freq[(b - b'a') as usize] += 1;
    }
    for (i, b) in s.bytes().enumerate() {
        if freq[(b - b'a') as usize] == 1 {
            return i as i32;
        }
    }
    -1
}
```

## TypeScript Implementation
```typescript
export function firstUniqChar(s: string): number {
    const freq = new Array(26).fill(0);
    const codeA = 'a'.charCodeAt(0);
    for (let i = 0; i < s.length; i++) {
        freq[s.charCodeAt(i) - codeA]++;
    }
    for (let i = 0; i < s.length; i++) {
        if (freq[s.charCodeAt(i) - codeA] === 1) return i;
    }
    return -1;
}
```
