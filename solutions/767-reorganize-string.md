# 767. Reorganize String

## Problem Statement
Given a string `s`, rearrange the characters of `s` so that any two adjacent characters are not the same. Return any possible rearrangement of `s` or return `""` if not possible.

---

## Method Explanation
1. Count character frequencies. If any character frequency exceeds `(n + 1) / 2`, valid rearrangement is impossible (Pigeonhole principle).
2. Insert characters into a max-heap keyed by remaining frequency.
3. In each step, pop the two most frequent characters, append both to the result string, decrement frequencies, and push back if positive.

---

## Rust Implementation

```rust
use std::collections::BinaryHeap;

pub struct Solution;

impl Solution {
    pub fn reorganize_string(s: String) -> String {
        let n = s.len();
        let mut counts = [0usize; 26];
        for b in s.bytes() {
            counts[(b - b'a') as usize] += 1;
        }

        let mut heap = BinaryHeap::new();
        for (i, &count) in counts.iter().enumerate() {
            if count > 0 {
                if count > (n + 1) / 2 {
                    return String::new();
                }
                heap.push((count, (b'a' + i as u8) as char));
            }
        }

        let mut result = String::with_capacity(n);
        while heap.len() >= 2 {
            let (count1, char1) = heap.pop().unwrap();
            let (count2, char2) = heap.pop().unwrap();

            result.push(char1);
            result.push(char2);

            if count1 > 1 {
                heap.push((count1 - 1, char1));
            }
            if count2 > 1 {
                heap.push((count2 - 1, char2));
            }
        }

        if let Some((_, char1)) = heap.pop() {
            result.push(char1);
        }

        result
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_reorganize() {
        let res = Solution::reorganize_string("aab".to_string());
        assert_eq!(res, "aba");
        let impossible = Solution::reorganize_string("aaab".to_string());
        assert_eq!(impossible, "");
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(N log K)` where `K <= 26` alphabet size, practically `O(N)`.
- Space Complexity: `O(K)` for frequency table and heap.
