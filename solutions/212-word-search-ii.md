# Problem 212: Word Search II

## Problem Statement
Given an `m x n` `board` of characters and a list of strings `words`, return all words on the board.

## Optimization
1. Insert all `words` into a Trie. Store the full word at the leaf node to avoid string reconstruction.
2. Backtrack over 2D grid. Prune branches immediately when grid character is not in current Trie node's children.
3. Once a word is matched, set node word reference to null to avoid duplicates and prune leaf.

## Complexity
- Time: $O(M \times N \times 4^{L})$ bounded strictly by Trie depth.
- Space: $O(\sum |words|)$ for Trie.

## C++ Implementation
```cpp
#include <vector>
#include <string>

struct TrieNode {
    TrieNode* children[26] = {nullptr};
    std::string word = "";
};

class Solution {
    void insert(TrieNode* root, const std::string& word) {
        TrieNode* curr = root;
        for (char c : word) {
            int idx = c - 'a';
            if (!curr->children[idx]) curr->children[idx] = new TrieNode();
            curr = curr->children[idx];
        }
        curr->word = word;
    }

    void dfs(std::vector<std::vector<char>>& board, int r, int c, TrieNode* node, std::vector<std::string>& result) {
        char ch = board[r][c];
        if (ch == '#' || !node->children[ch - 'a']) return;

        node = node->children[ch - 'a'];
        if (!node->word.empty()) {
            result.push_back(node->word);
            node->word.clear(); // Avoid duplicates
        }

        board[r][c] = '#';
        static const int dr[] = {-1, 1, 0, 0};
        static const int dc[] = {0, 0, -1, 1};

        for (int i = 0; i < 4; ++i) {
            int nr = r + dr[i];
            int nc = c + dc[i];
            if (nr >= 0 && nr < static_cast<int>(board.size()) &&
                nc >= 0 && nc < static_cast<int>(board[0].size())) {
                dfs(board, nr, nc, node, result);
            }
        }
        board[r][c] = ch;
    }

public:
    std::vector<std::string> findWords(std::vector<std::vector<char>>& board, const std::vector<std::string>& words) {
        TrieNode* root = new TrieNode();
        for (const auto& w : words) insert(root, w);

        std::vector<std::string> result;
        for (int r = 0; r < static_cast<int>(board.size()); ++r) {
            for (int c = 0; c < static_cast<int>(board[0].size()); ++c) {
                dfs(board, r, c, root, result);
            }
        }
        return result;
    }
};
```
