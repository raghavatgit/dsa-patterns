# Problem 543: Diameter of Binary Tree

## Problem Statement
Given the root of a binary tree, return the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree.

## Complexity
- Time: $O(N)$
- Space: $O(H)$

## C++ Implementation
```cpp
#include <algorithm>

class Solution {
    int max_diameter = 0;

    int depth(TreeNode* node) {
        if (!node) return 0;
        int left = depth(node->left);
        int right = depth(node->right);
        max_diameter = std::max(max_diameter, left + right);
        return 1 + std::max(left, right);
    }

public:
    int diameterOfBinaryTree(TreeNode* root) {
        depth(root);
        return max_diameter;
    }
};
```
