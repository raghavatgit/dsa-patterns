# 208. Implement Trie (Prefix Tree)

## Complexity
- Time Complexity: O(L) for insert, search, startsWith
- Space Complexity: O(N * L)

## TypeScript Implementation
```typescript
class TrieNode {
    children: Record<string, TrieNode> = {};
    isEnd = false;
}

export class Trie {
    private root = new TrieNode();

    insert(word: string): void {
        let curr = this.root;
        for (const c of word) {
            if (!curr.children[c]) curr.children[c] = new TrieNode();
            curr = curr.children[c];
        }
        curr.isEnd = true;
    }

    search(word: string): boolean {
        let curr = this.root;
        for (const c of word) {
            if (!curr.children[c]) return false;
            curr = curr.children[c];
        }
        return curr.isEnd;
    }

    startsWith(prefix: string): boolean {
        let curr = this.root;
        for (const c of prefix) {
            if (!curr.children[c]) return false;
            curr = curr.children[c];
        }
        return true;
    }
}
```
