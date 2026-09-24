# Problem 124: Binary Tree Maximum Path Sum

## Problem Statement
A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Return the maximum path sum of any non-empty path.

## Post-Order Formulation
At each node:
- Compute maximum gain from left subtree: `max(0, dfs(node->left))`.
- Compute maximum gain from right subtree: `max(0, dfs(node->right))`.
- Candidate path through current node: `node->val + left_gain + right_gain`. Update global max.
- Return to parent: `node->val + max(left_gain, right_gain)`.

## Complexity
- Time: $O(N)$
- Space: $O(H)$

## C++ Implementation
```cpp
#include <algorithm>
#include <climits>

class Solution {
    int max_sum = INT_MIN;

    int maxGain(TreeNode* node) {
        if (!node) return 0;

        int left_gain = std::max(0, maxGain(node->left));
        int right_gain = std::max(0, maxGain(node->right));

        int path_through_root = node->val + left_gain + right_gain;
        max_sum = std::max(max_sum, path_through_root);

        return node->val + std::max(left_gain, right_gain);
    }

public:
    int maxPathSum(TreeNode* root) {
        maxGain(root);
        return max_sum;
    }
};
```
