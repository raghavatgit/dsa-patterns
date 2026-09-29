# 211. Design Add and Search Words Data Structure

## Complexity
- Time Complexity: O(M) without wildcards, O(26^K) with K wildcards
- Space Complexity: O(total characters)

## TypeScript Implementation
```typescript
class WordDictionaryNode {
    children: Record<string, WordDictionaryNode> = {};
    isEnd = false;
}

export class WordDictionary {
    private root = new WordDictionaryNode();

    addWord(word: string): void {
        let curr = this.root;
        for (const c of word) {
            if (!curr.children[c]) curr.children[c] = new WordDictionaryNode();
            curr = curr.children[c];
        }
        curr.isEnd = true;
    }

    search(word: string): boolean {
        const dfs = (node: WordDictionaryNode, idx: number): boolean => {
            if (idx === word.length) return node.isEnd;
            const c = word[idx];
            if (c === '.') {
                for (const child of Object.values(node.children)) {
                    if (dfs(child, idx + 1)) return true;
                }
                return false;
            } else {
                if (!node.children[c]) return false;
                return dfs(node.children[c], idx + 1);
            }
        };
        return dfs(this.root, 0);
    }
}
```
