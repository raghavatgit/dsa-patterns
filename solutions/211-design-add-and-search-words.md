# Problem 211: Design Add and Search Words Data Structure

## Problem Statement
Design a data structure that supports adding new words and finding if a string matches any previously added string, where `.` can match any letter.

## Approach
Trie with DFS branch traversal for `.`.
When matching a standard letter, transition to that specific child.
When matching `.`, recursively search all non-null children; return true if any path matches.

## Complexity
- `addWord`: $O(L)$ time.
- `search`: $O(26^D \times L)$ in worst case where $D$ is count of dots, but $O(L)$ on average.

## C++ Implementation
```cpp
#include <string>

class WordDictionary {
private:
    struct Node {
        Node* children[26] = {nullptr};
        bool is_end = false;
        ~Node() {
            for (int i = 0; i < 26; ++i) delete children[i];
        }
    };

    Node* root;

    bool searchInNode(const std::string& word, int idx, Node* curr) const {
        if (!curr) return false;
        if (idx == static_cast<int>(word.length())) return curr->is_end;

        char c = word[idx];
        if (c != '.') {
            int c_idx = c - 'a';
            return searchInNode(word, idx + 1, curr->children[c_idx]);
        }

        for (int i = 0; i < 26; ++i) {
            if (curr->children[i] && searchInNode(word, idx + 1, curr->children[i])) {
                return true;
            }
        }
        return false;
    }

public:
    WordDictionary() : root(new Node()) {}
    ~WordDictionary() { delete root; }

    void addWord(const std::string& word) {
        Node* curr = root;
        for (char c : word) {
            int idx = c - 'a';
            if (!curr->children[idx]) curr->children[idx] = new Node();
            curr = curr->children[idx];
        }
        curr->is_end = true;
    }

    bool search(const std::string& word) const {
        return searchInNode(word, 0, root);
    }
};
```
