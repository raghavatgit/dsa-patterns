# Problem 226: Invert Binary Tree

## Problem Statement
Given the root of a binary tree, invert the tree, and return its root.

## Complexity
- Time: $O(N)$
- Space: $O(H)$ recursion stack

## C++ Implementation
```cpp
TreeNode* invertTree(TreeNode* root) {
    if (!root) return nullptr;

    TreeNode* temp = root->left;
    root->left = invertTree(root->right);
    root->right = invertTree(temp);

    return root;
}
```
