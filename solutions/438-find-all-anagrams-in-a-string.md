# 438. Find All Anagrams in a String

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn find_anagrams(s: String, p: String) -> Vec<i32> {
    let s_bytes = s.as_bytes();
    let p_bytes = p.as_bytes();
    if s_bytes.len() < p_bytes.len() {
        return vec![];
    }
    let mut p_count = [0i32; 26];
    let mut s_count = [0i32; 26];
    for &b in p_bytes {
        p_count[(b - b'a') as usize] += 1;
    }
    let k = p_bytes.len();
    for i in 0..k {
        s_count[(s_bytes[i] - b'a') as usize] += 1;
    }
    let mut res = Vec::new();
    if s_count == p_count {
        res.push(0);
    }
    for i in k..s_bytes.len() {
        s_count[(s_bytes[i] - b'a') as usize] += 1;
        s_count[(s_bytes[i - k] - b'a') as usize] -= 1;
        if s_count == p_count {
            res.push((i - k + 1) as i32);
        }
    }
    res
}
```

## TypeScript Implementation
```typescript
export function findAnagrams(s: string, p: string): number[] {
    if (s.length < p.length) return [];
    const pCount = new Array(26).fill(0);
    const sCount = new Array(26).fill(0);
    const codeA = 'a'.charCodeAt(0);

    for (let i = 0; i < p.length; i++) {
        pCount[p.charCodeAt(i) - codeA]++;
        sCount[s.charCodeAt(i) - codeA]++;
    }

    const res: number[] = [];
    const matches = (a: number[], b: number[]) => a.every((v, idx) => v === b[idx]);

    if (matches(sCount, pCount)) res.push(0);

    for (let i = p.length; i < s.length; i++) {
        sCount[s.charCodeAt(i) - codeA]++;
        sCount[s.charCodeAt(i - p.length) - codeA]--;
        if (matches(sCount, pCount)) {
            res.push(i - p.length + 1);
        }
    }
    return res;
}
```
