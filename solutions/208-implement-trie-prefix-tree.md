# Problem 208: Implement Trie (Prefix Tree)

## Problem Statement
A trie (pronounced as 'try') or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. Implement the `Trie` class supporting `insert`, `search`, and `startsWith`.

## Complexity
- Insert: $O(L)$ time, $O(L)$ space where $L$ is word length.
- Search: $O(L)$ time, $O(1)$ auxiliary space.
- StartsWith: $O(L)$ time, $O(1)$ auxiliary space.

## C++ Implementation
```cpp
#include <string>
#include <vector>
#include <memory>

class Trie {
private:
    struct TrieNode {
        TrieNode* children[26] = {nullptr};
        bool is_end_of_word = false;

        ~TrieNode() {
            for (int i = 0; i < 26; ++i) {
                delete children[i];
            }
        }
    };

    TrieNode* root;

public:
    Trie() : root(new TrieNode()) {}
    ~Trie() { delete root; }

    void insert(const std::string& word) {
        TrieNode* curr = root;
        for (char c : word) {
            int idx = c - 'a';
            if (!curr->children[idx]) {
                curr->children[idx] = new TrieNode();
            }
            curr = curr->children[idx];
        }
        curr->is_end_of_word = true;
    }

    bool search(const std::string& word) const {
        TrieNode* curr = root;
        for (char c : word) {
            int idx = c - 'a';
            if (!curr->children[idx]) return false;
            curr = curr->children[idx];
        }
        return curr->is_end_of_word;
    }

    bool startsWith(const std::string& prefix) const {
        TrieNode* curr = root;
        for (char c : prefix) {
            int idx = c - 'a';
            if (!curr->children[idx]) return false;
            curr = curr->children[idx];
        }
        return true;
    }
};
```
