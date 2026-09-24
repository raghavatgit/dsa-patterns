# Problem 105: Construct Binary Tree from Preorder and Inorder Traversal

## Problem Statement
Given two integer arrays `preorder` and `inorder`, construct and return the binary tree.

## Approach
- First element of `preorder` is the root.
- Find root in `inorder` using hash map.
- Left of root in `inorder` corresponds to left subtree of size $K$.
- Recurse on left subtree and right subtree with partitioned slices.

## Complexity
- Time: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <unordered_map>

class Solution {
    std::unordered_map<int, int> in_map;
    int pre_idx = 0;

    TreeNode* build(const std::vector<int>& preorder, int in_left, int in_right) {
        if (in_left > in_right) return nullptr;

        int root_val = preorder[pre_idx++];
        TreeNode* root = new TreeNode(root_val);
        int mid = in_map[root_val];

        root->left = build(preorder, in_left, mid - 1);
        root->right = build(preorder, mid + 1, in_right);
        return root;
    }

public:
    TreeNode* buildTree(std::vector<int>& preorder, std::vector<int>& inorder) {
        in_map.clear();
        pre_idx = 0;
        for (int i = 0; i < static_cast<int>(inorder.size()); ++i) {
            in_map[inorder[i]] = i;
        }
        return build(preorder, 0, inorder.size() - 1);
    }
};
```
