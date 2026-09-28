# 567. Permutation in String

## Problem Statement
Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

---

## TypeScript Implementation

```typescript
export function checkInclusion(s1: string, s2: string): boolean {
  const n1 = s1.length;
  const n2 = s2.length;
  if (n1 > n2) return false;

  const count1 = new Array<number>(26).fill(0);
  const count2 = new Array<number>(26).fill(0);
  const codeA = 'a'.charCodeAt(0);

  for (let i = 0; i < n1; i++) {
    count1[s1.charCodeAt(i) - codeA]++;
    count2[s2.charCodeAt(i) - codeA]++;
  }

  let matches = 0;
  for (let i = 0; i < 26; i++) {
    if (count1[i] === count2[i]) matches++;
  }

  for (let i = n1; i < n2; i++) {
    if (matches === 26) return true;

    const rIdx = s2.charCodeAt(i) - codeA;
    count2[rIdx]++;
    if (count2[rIdx] === count1[rIdx]) {
      matches++;
    } else if (count2[rIdx] === count1[rIdx] + 1) {
      matches--;
    }

    const lIdx = s2.charCodeAt(i - n1) - codeA;
    count2[lIdx]--;
    if (count2[lIdx] === count1[lIdx]) {
      matches++;
    } else if (count2[lIdx] === count1[lIdx] - 1) {
      matches--;
    }
  }

  return matches === 26;
}
```

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn check_inclusion(s1: String, s2: String) -> bool {
        let b1 = s1.as_bytes();
        let b2 = s2.as_bytes();
        let (n1, n2) = (b1.len(), b2.len());

        if n1 > n2 {
            return false;
        }

        let mut c1 = [0i32; 26];
        let mut c2 = [0i32; 26];

        for i in 0..n1 {
            c1[(b1[i] - b'a') as usize] += 1;
            c2[(b2[i] - b'a') as usize] += 1;
        }

        let mut matches = 0;
        for i in 0..26 {
            if c1[i] == c2[i] {
                matches += 1;
            }
        }

        for i in n1..n2 {
            if matches == 26 {
                return true;
            }

            let r = (b2[i] - b'a') as usize;
            c2[r] += 1;
            if c2[r] == c1[r] {
                matches += 1;
            } else if c2[r] == c1[r] + 1 {
                matches -= 1;
            }

            let l = (b2[i - n1] - b'a') as usize;
            c2[l] -= 1;
            if c2[l] == c1[l] {
                matches += 1;
            } else if c2[l] == c1[l] - 1 {
                matches -= 1;
            }
        }

        matches == 26
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(n2)` with `O(1)` per window slide due to `matches` tracking.
- Space Complexity: `O(1)` using two 26-element frequency arrays.
