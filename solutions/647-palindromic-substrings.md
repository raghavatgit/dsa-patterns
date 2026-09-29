# 647. Palindromic Substrings

## Complexity
- Time Complexity: O(n^2)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn count_substrings(s: String) -> i32 {
    let bytes = s.as_bytes();
    let n = bytes.len();
    let mut count = 0;

    fn expand(bytes: &[u8], mut l: i32, mut r: i32) -> i32 {
        let mut ans = 0;
        while l >= 0 && (r as usize) < bytes.len() && bytes[l as usize] == bytes[r as usize] {
            ans += 1;
            l -= 1;
            r += 1;
        }
        ans
    }

    for i in 0..n {
        count += expand(bytes, i as i32, i as i32);
        count += expand(bytes, i as i32, (i + 1) as i32);
    }
    count
}
```

## TypeScript Implementation
```typescript
export function countSubstrings(s: string): number {
    let count = 0;
    const expand = (l: number, r: number): number => {
        let matches = 0;
        while (l >= 0 && r < s.length && s[l] === s[r]) {
            matches++;
            l--;
            r++;
        }
        return matches;
    };
    for (let i = 0; i < s.length; i++) {
        count += expand(i, i);
        count += expand(i, i + 1);
    }
    return count;
}
```
