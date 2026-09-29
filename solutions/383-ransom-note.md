# 383. Ransom Note

## Complexity
- Time Complexity: O(m + n)
- Space Complexity: O(1) fixed 26 characters

## Rust Implementation
```rust
pub fn can_construct(ransom_note: String, magazine: String) -> bool {
    let mut counts = [0i32; 26];
    for b in magazine.bytes() {
        counts[(b - b'a') as usize] += 1;
    }
    for b in ransom_note.bytes() {
        let idx = (b - b'a') as usize;
        counts[idx] -= 1;
        if counts[idx] < 0 {
            return false;
        }
    }
    true
}
```

## TypeScript Implementation
```typescript
export function canConstruct(ransomNote: string, magazine: string): boolean {
    const counts = new Array(26).fill(0);
    const codeA = 'a'.charCodeAt(0);
    for (let i = 0; i < magazine.length; i++) {
        counts[magazine.charCodeAt(i) - codeA]++;
    }
    for (let i = 0; i < ransomNote.length; i++) {
        const idx = ransomNote.charCodeAt(i) - codeA;
        counts[idx]--;
        if (counts[idx] < 0) return false;
    }
    return true;
}
```
