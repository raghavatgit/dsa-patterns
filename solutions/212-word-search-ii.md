# 212. Word Search II

## Complexity
- Time Complexity: O(m * n * 4^L) bounded by Trie depth
- Space Complexity: O(total characters in words)

## TypeScript Implementation
```typescript
export function findWords(board: string[][], words: string[]): string[] {
    const root = new TrieNode();
    for (const w of words) {
        let curr = root;
        for (const c of w) {
            if (!curr.children[c]) curr.children[c] = new TrieNode();
            curr = curr.children[c];
        }
        curr.word = w;
    }

    const m = board.length, n = board[0].length;
    const res: string[] = [];

    const dfs = (r: number, c: number, node: TrieNode) => {
        const ch = board[r][c];
        if (!node.children[ch]) return;
        const nextNode = node.children[ch];
        if (nextNode.word) {
            res.push(nextNode.word);
            nextNode.word = null; // Prevent duplicates
        }

        board[r][c] = '#';
        const dirs = [[0, 1], [0, -1], [1, 0], [-1, 0]];
        for (const [dr, dc] of dirs) {
            const nr = r + dr, nc = c + dc;
            if (nr >= 0 && nr < m && nc >= 0 && nc < n && board[nr][nc] !== '#') {
                dfs(nr, nc, nextNode);
            }
        }
        board[r][c] = ch;
    };

    for (let r = 0; r < m; r++) {
        for (let c = 0; c < n; c++) {
            dfs(r, c, root);
        }
    }

    return res;
}
```
