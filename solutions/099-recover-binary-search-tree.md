# Problem 099: Recover Binary Search Tree

## Problem Statement
You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake. Recover the tree without changing its structure in $O(1)$ space.

## Morris Inorder Traversal
An inorder traversal of a BST yields a strictly increasing sequence.
A single swap creates at most two points where `prev->val > curr->val`:
- First violation: record `first = prev`, `second = curr`.
- Second violation: update `second = curr`.
Swap `first->val` and `second->val`.

## Complexity
- Time: $O(N)$
- Space: $O(1)$ auxiliary space using Morris threaded pointers.

## C++ Implementation
```cpp
#include <algorithm>

class Solution {
public:
    void recoverTree(TreeNode* root) {
        TreeNode* first = nullptr;
        TreeNode* second = nullptr;
        TreeNode* prev = nullptr;
        TreeNode* curr = root;

        while (curr) {
            if (!curr->left) {
                if (prev && prev->val > curr->val) {
                    if (!first) first = prev;
                    second = curr;
                }
                prev = curr;
                curr = curr->right;
            } else {
                TreeNode* pred = curr->left;
                while (pred->right && pred->right != curr) {
                    pred = pred->right;
                }

                if (!pred->right) {
                    pred->right = curr;
                    curr = curr->left;
                } else {
                    pred->right = nullptr;
                    if (prev && prev->val > curr->val) {
                        if (!first) first = prev;
                        second = curr;
                    }
                    prev = curr;
                    curr = curr->right;
                }
            }
        }

        if (first && second) {
            std::swap(first->val, second->val);
        }
    }
};
```
