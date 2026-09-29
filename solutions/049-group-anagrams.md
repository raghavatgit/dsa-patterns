# 49. Group Anagrams

## Complexity
- Time Complexity: O(n * k log k) or O(n * k) with character frequency counting
- Space Complexity: O(n * k) for hash map storage

## Rust Implementation
```rust
use std::collections::HashMap;

pub fn group_anagrams(strs: Vec<String>) -> Vec<Vec<String>> {
    let mut map: HashMap<String, Vec<String>> = HashMap::new();

    for s in strs {
        let mut chars: Vec<char> = s.chars().collect();
        chars.sort_unstable();
        let key: String = chars.into_iter().collect();
        map.entry(key).or_default().push(s);
    }

    map.into_values().collect()
}
```

## TypeScript Implementation
```typescript
export function groupAnagrams(strs: string[]): string[][] {
    const map = new Map<string, string[]>();

    for (const str of strs) {
        const key = str.split('').sort().join('');
        if (!map.has(key)) map.set(key, []);
        map.get(key)!.push(str);
    }

    return Array.from(map.values());
}
```
