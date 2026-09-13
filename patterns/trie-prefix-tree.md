# Trie (Prefix Tree) Pattern

## Concept
A Trie (retrieval tree) is an ordered tree data structure used to store an associative array where keys are usually strings. Unlike a binary search tree, no node in the tree stores the key associated with that node; instead, its position in the tree defines the key.

Tries excel at prefix matching, autocomplete dictionaries, and IP routing tables with O(L) complexity, where L is the key length.

## TypeScript Implementation

```typescript
class TrieNode {
  children: Map<string, TrieNode> = new Map();
  isEndOfWord: boolean = false;
}

export class Trie {
  private root: TrieNode = new TrieNode();

  insert(word: string): void {
    let current = this.root;
    for (const char of word) {
      if (!current.children.has(char)) {
        current.children.set(char, new TrieNode());
      }
      current = current.children.get(char)!;
    }
    current.isEndOfWord = true;
  }

  search(word: string): boolean {
    const node = this.traversePrefix(word);
    return node !== null && node.isEndOfWord;
  }

  startsWith(prefix: string): boolean {
    return this.traversePrefix(prefix) !== null;
  }

  private traversePrefix(prefix: string): TrieNode | null {
    let current = this.root;
    for (const char of prefix) {
      if (!current.children.has(char)) {
        return null;
      }
      current = current.children.get(char)!;
    }
    return current;
  }
}
```

## Rust Implementation

```rust
use std::collections::HashMap;

#[derive(Default, Debug)]
pub struct TrieNode {
    pub children: HashMap<char, TrieNode>,
    pub is_end_of_word: bool,
}

#[derive(Default, Debug)]
pub struct Trie {
    root: TrieNode,
}

impl Trie {
    pub fn new() -> Self {
        Trie { root: TrieNode::default() }
    }

    pub fn insert(&mut self, word: &str) {
        let mut curr = &mut self.root;
        for ch in word.chars() {
            curr = curr.children.entry(ch).or_default();
        }
        curr.is_end_of_word = true;
    }

    pub fn search(&self, word: &str) -> bool {
        self.traverse(word).map_or(false, |node| node.is_end_of_word)
    }

    pub fn starts_with(&self, prefix: &str) -> bool {
        self.traverse(prefix).is_some()
    }

    fn traverse(&self, prefix: &str) -> Option<&TrieNode> {
        let mut curr = &self.root;
        for ch in prefix.chars() {
            curr = curr.children.get(&ch)?;
        }
        Some(curr)
    }
}
```

## Complexity Analysis
* **Insertion Time:** O(L) where L is string length.
* **Search / StartsWith Time:** O(L) independent of the number of words stored.
* **Space Complexity:** O(ALPHA_SIZE * L * N) worst case for disjoint alphabets.
