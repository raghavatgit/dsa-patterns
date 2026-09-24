# Problem 114: Flatten Binary Tree to Linked List

## Problem Statement
Given the `root` of a binary tree, flatten the tree into a 'linked list' in-place using preorder traversal order.

## In-Place Morris Traversal
At each node with a non-null `left` child:
1. Find rightmost predecessor in `left` subtree.
2. Link predecessor's `right` to current node's `right`.
3. Move `left` subtree to `right`, and set `left` to null.
4. Advance current pointer to `right`.

## Complexity
- Time: $O(N)$
- Space: $O(1)$ auxiliary space

## C++ Implementation
```cpp
void flatten(TreeNode* root) {
    TreeNode* curr = root;
    while (curr) {
        if (curr->left) {
            TreeNode* pred = curr->left;
            while (pred->right) pred = pred->right;
            pred->right = curr->right;
            curr->right = curr->left;
            curr->left = nullptr;
        }
        curr = curr->right;
    }
}
```
