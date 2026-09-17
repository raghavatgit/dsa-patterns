# Problem: Word Ladder

## Problem Statement
A transformation sequence from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:
- Every adjacent pair of words differs by a single letter.
- Every `si` for `1 <= i <= k` is in `wordList`.
- Return the number of words in the shortest transformation sequence, or 0 if no sequence exists.

## Intuition & Approach
Bidirectional Breadth-First Search (BFS):
1. Convert `wordList` into a hash set for $O(1)$ lookup. If `endWord` is not present, return 0 immediately.
2. Run two search frontiers: `beginSet` starting from `beginWord` and `endSet` starting from `endWord`.
3. Always expand the smaller frontier to minimize branching factor: $O(b^{d/2})$ vs $O(b^d)$.
4. For each word in the active frontier, mutate each character from 'a' to 'z'. If a mutated word is in the opposing set, the paths connect: return current length + 1.
5. Time Complexity: $O(M^2 \times N)$ where $M$ is word length and $N$ is dictionary size. Space Complexity: $O(M \times N)$.

## TypeScript Implementation

```typescript
export function ladderLength(beginWord: string, endWord: string, wordList: string[]): number {
  const dict = new Set(wordList);
  if (!dict.has(endWord)) return 0;

  let beginSet = new Set<string>([beginWord]);
  let endSet = new Set<string>([endWord]);
  let visited = new Set<string>([beginWord, endWord]);
  let step = 1;

  while (beginSet.size > 0 && endSet.size > 0) {
    if (beginSet.size > endSet.size) {
      const temp = beginSet;
      beginSet = endSet;
      endSet = temp;
    }

    const nextLevel = new Set<string>();

    for (const word of beginSet) {
      const chars = word.split("");
      for (let i = 0; i < chars.length; i++) {
        const originalChar = chars[i];
        for (let c = 97; c <= 122; c++) {
          const ch = String.fromCharCode(c);
          if (ch === originalChar) continue;

          chars[i] = ch;
          const candidate = chars.join("");

          if (endSet.has(candidate)) {
            return step + 1;
          }

          if (dict.has(candidate) && !visited.has(candidate)) {
            visited.add(candidate);
            nextLevel.add(candidate);
          }
        }
        chars[i] = originalChar;
      }
    }

    beginSet = nextLevel;
    step++;
  }

  return 0;
}
```

## Rust Implementation

```rust
use std::collections::HashSet;

pub fn ladder_length(begin_word: String, end_word: String, word_list: Vec<String>) -> i32 {
    let dict: HashSet<String> = word_list.into_iter().collect();
    if !dict.contains(&end_word) {
        return 0;
    }

    let mut begin_set = HashSet::new();
    begin_set.insert(begin_word.clone());

    let mut end_set = HashSet::new();
    end_set.insert(end_word.clone());

    let mut visited = HashSet::new();
    visited.insert(begin_word);
    visited.insert(end_word);

    let mut step = 1;

    while !begin_set.is_empty() && !end_set.is_empty() {
        if begin_set.len() > end_set.len() {
            std::mem::swap(&mut begin_set, &mut end_set);
        }

        let mut next_level = HashSet::new();

        for word in &begin_set {
            let mut chars: Vec<char> = word.chars().collect();
            for i in 0..chars.len() {
                let orig = chars[i];
                for c in b'a'..=b'z' {
                    let ch = c as char;
                    if ch == orig {
                        continue;
                    }
                    chars[i] = ch;
                    let candidate: String = chars.iter().collect();

                    if end_set.contains(&candidate) {
                        return step + 1;
                    }

                    if dict.contains(&candidate) && !visited.contains(&candidate) {
                        visited.insert(candidate.clone());
                        next_level.insert(candidate);
                    }
                }
                chars[i] = orig;
            }
        }

        begin_set = next_level;
        step += 1;
    }

    0
}
```
