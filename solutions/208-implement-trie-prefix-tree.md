# Problem: Implement Trie (Prefix Tree)

## Problem Statement
A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. Implement the `Trie` class with `insert(word)`, `search(word)`, and `startsWith(prefix)` methods.

## Intuition & Approach
Array-Backed 26-Way Node Structure:
1. Each node contains an array `children` of 26 pointers for lowercase English letters 'a' through 'z', and a boolean flag `is_end`.
2. `insert(word)`: Traverse character by character. If child pointer at index `ch - 'a'` is null, instantiate a new node. Mark terminal node `is_end = true`.
3. `search(word)`: Traverse character by character. If any pointer is null, return `false`. Return `node.is_end` at the terminus.
4. `startsWith(prefix)`: Traverse prefix. If all characters exist, return `true`.
5. Time Complexity: $O(L)$ for each operation, where $L$ is word length. Space Complexity: $O(\Sigma \times N \times L)$ for node allocations.

## TypeScript Implementation

```typescript
class TrieNode {
  children: (TrieNode | null)[] = new Array(26).fill(null);
  isEnd: boolean = false;
}

export class Trie {
  private root: TrieNode = new TrieNode();

  insert(word: string): void {
    let curr = this.root;
    for (let i = 0; i < word.length; i++) {
      const idx = word.charCodeAt(i) - 97;
      if (!curr.children[idx]) {
        curr.children[idx] = new TrieNode();
      }
      curr = curr.children[idx]!;
    }
    curr.isEnd = true;
  }

  search(word: string): boolean {
    let curr = this.root;
    for (let i = 0; i < word.length; i++) {
      const idx = word.charCodeAt(i) - 97;
      if (!curr.children[idx]) return false;
      curr = curr.children[idx]!;
    }
    return curr.isEnd;
  }

  startsWith(prefix: string): boolean {
    let curr = this.root;
    for (let i = 0; i < prefix.length; i++) {
      const idx = prefix.charCodeAt(i) - 97;
      if (!curr.children[idx]) return false;
      curr = curr.children[idx]!;
    }
    return true;
  }
}
```

## Rust Implementation

```rust
#[derive(Default)]
pub struct TrieNode {
    children: [Option<Box<TrieNode>>; 26],
    is_end: bool,
}

#[derive(Default)]
pub struct Trie {
    root: TrieNode,
}

impl Trie {
    pub fn new() -> Self {
        Self::default()
    }

    pub fn insert(&mut self, word: String) {
        let mut curr = &mut self.root;
        for b in word.bytes() {
            let idx = (b - b'a') as usize;
            curr = curr.children[idx].get_or_insert_with(Box::default);
        }
        curr.is_end = true;
    }

    pub fn search(&self, word: String) -> bool {
        let mut curr = &self.root;
        for b in word.bytes() {
            let idx = (b - b'a') as usize;
            match &curr.children[idx] {
                Some(next) => curr = next,
                None => return false,
            }
        }
        curr.is_end
    }

    pub fn starts_with(&self, prefix: String) -> bool {
        let mut curr = &self.root;
        for b in prefix.bytes() {
            let idx = (b - b'a') as usize;
            match &curr.children[idx] {
                Some(next) => curr = next,
                None => return false,
            }
        }
        true
    }
}
```
