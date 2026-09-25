# Problem 102: Binary Tree Level Order Traversal

## Problem Statement
Given the root of a binary tree, return the level order traversal of its nodes' values (i.e., from left to right, level by level).

## Approach
FIFO Queue with Level Sizing:
At the start of each level loop, capture `level_size = q.size()`.
Dequeue exactly `level_size` nodes, record their values, and enqueue children.

## Complexity
- Time: $O(N)$
- Space: $O(N)$ for queue

## C++ Implementation
```cpp
#include <vector>
#include <queue>

std::vector<std::vector<int>> levelOrder(TreeNode* root) {
    if (!root) return {};

    std::vector<std::vector<int>> result;
    std::queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int levelSize = q.size();
        std::vector<int> currentLevel;
        currentLevel.reserve(levelSize);

        for (int i = 0; i < levelSize; ++i) {
            TreeNode* node = q.front();
            q.pop();
            currentLevel.push_back(node->val);

            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        result.push_back(std::move(currentLevel));
    }

    return result;
}
```
