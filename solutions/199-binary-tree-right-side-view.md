# Problem 199: Binary Tree Right Side View

## Problem Statement
Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

## Reverse Preorder DFS (Root -> Right -> Left)
Traverse the right child before the left child:
The first node encountered at depth $D$ is guaranteed to be the rightmost visible node.
If `depth == result.size()`, append `node->val`.

## Complexity
- Time: $O(N)$
- Space: $O(H)$

## C++ Implementation
```cpp
#include <vector>

class Solution {
    void dfs(TreeNode* node, int depth, std::vector<int>& result) {
        if (!node) return;

        if (depth == static_cast<int>(result.size())) {
            result.push_back(node->val);
        }

        dfs(node->right, depth + 1, result);
        dfs(node->left, depth + 1, result);
    }

public:
    std::vector<int> rightSideView(TreeNode* root) {
        std::vector<int> result;
        dfs(root, 0, result);
        return result;
    }
};
```
