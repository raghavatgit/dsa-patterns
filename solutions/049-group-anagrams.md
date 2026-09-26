# 049. Group Anagrams

## Problem Statement
Given an array of strings `strs`, group the anagrams together. You can return the answer in any order. An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

---

## Optimal Architecture: Frequency Array Key

Sorting each string takes `O(K log K)` where `K` is string length. For long strings, we can achieve `O(K)` by hashing a 26-element character frequency array as the map key.

---

## TypeScript Implementation

```typescript
export function groupAnagrams(strs: string[]): string[][] {
  const map = new Map<string, string[]>();

  for (const s of strs) {
    const count = new Array(26).fill(0);
    for (let i = 0; i < s.length; i++) {
      count[s.charCodeAt(i) - 97]++;
    }
    
    // Construct serialized key delimiter-separated to prevent ambiguous counts
    const key = count.join('#');
    
    if (!map.has(key)) {
      map.set(key, []);
    }
    map.get(key)!.push(s);
  }

  return Array.from(map.values());
}
```

---

## Rust Implementation

```rust
use std::collections::HashMap;

pub fn group_anagrams(strs: Vec<String>) -> Vec<Vec<String>> {
    let mut map: HashMap<[u8; 26], Vec<String>> = HashMap::new();

    for s in strs {
        let mut count = [0u8; 26];
        for b in s.bytes() {
            count[(b - b'a') as usize] += 1;
        }
        map.entry(count).or_default().push(s);
    }

    map.into_values().collect()
}
```

---

## Complexity Analysis

* **Time Complexity:** `O(N * K)` where `N` is the number of strings and `K` is the maximum string length. Avoids `O(N * K log K)` sort overhead.
* **Space Complexity:** `O(N * K)` to store strings in bucketed hash table partitions.
