# Problem: Word Search II (Trie Backtracking)

## Problem Statement
Given an `m x n` `board` of characters and a list of strings `words`, return all words on the board. Each word must be constructed from letters of sequentially adjacent cells (horizontally or vertically neighboring). The same letter cell may not be used more than once in a word.

## Intuition & Approach
Trie-Guided Depth First Search:
1. Insert all dictionary words into a Trie. Store the complete word at the terminal node to eliminate string concatenation overhead.
2. Iterate through each cell `(r, c)` of the board. If the character exists in the Trie root, start DFS exploration.
3. DFS Backtracking:
   - Save current cell character and replace with '#' to mark visited in-place (saving $O(M \times N)$ auxiliary space).
   - If current Trie node contains a finished word, add it to results and set `node.word = null` to prevent duplicate captures.
   - Traverse 4 adjacent neighbours matching children of current Trie node.
   - Restore cell character upon backtracking.
4. Pruning optimization: When a leaf node is consumed, prune it from its parent to prevent redundant paths.
5. Time Complexity: $O(M \times N \times 4 \times 3^{L-1})$ where $L$ is maximum word length. Space Complexity: $O(\sum \text{len}(words))$ for Trie storage.

## TypeScript Implementation

```typescript
class TrieNode {
  children: Map<string, TrieNode> = new Map();
  word: string | null = null;
}

export function findWords(board: string[][], words: string[]): string[] {
  const root = new TrieNode();

  for (const w of words) {
    let node = root;
    for (const ch of w) {
      if (!node.children.has(ch)) {
        node.children.set(ch, new TrieNode());
      }
      node = node.children.get(ch)!;
    }
    node.word = w;
  }

  const results: string[] = [];
  const m = board.length;
  const n = board[0].length;

  function dfs(r: number, c: number, parent: TrieNode) {
    const ch = board[r][c];
    const currNode = parent.children.get(ch);
    if (!currNode) return;

    if (currNode.word !== null) {
      results.push(currNode.word);
      currNode.word = null;
    }

    board[r][c] = "#";

    const dirs = [[0, 1], [0, -1], [1, 0], [-1, 0]];
    for (const [dr, dc] of dirs) {
      const nr = r + dr;
      const nc = c + dc;
      if (nr >= 0 && nr < m && nc >= 0 && nc < n && board[nr][nc] !== "#") {
        dfs(nr, nc, currNode);
      }
    }

    board[r][c] = ch;

    if (currNode.children.size === 0) {
      parent.children.delete(ch);
    }
  }

  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      if (root.children.has(board[r][c])) {
        dfs(r, c, root);
      }
    }
  }

  return results;
}
```
