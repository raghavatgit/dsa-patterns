# Problem 236: Lowest Common Ancestor of a Binary Tree

## Problem Statement
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes `p` and `q`.

## Approach
Post-order recursive traversal:
- If current node is null or matches `p` or `q`, return current node.
- Recurse on `left` and `right` subtrees.
- If both subtrees return non-null, current node is the LCA.
- Otherwise, propagate the non-null child result.

## Complexity
- Time: $O(N)$
- Space: $O(H)$ recursion stack

## C++ Implementation
```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (!root || root == p || root == q) return root;

        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);

        if (left && right) return root;
        return left ? left : right;
    }
};
```
