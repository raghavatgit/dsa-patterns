# Problem 103: Binary Tree Zigzag Level Order Traversal

## Problem Statement
Given the root of a binary tree, return the zigzag level order traversal of its nodes' values (i.e., from left to right, then right to left for the next level and alternate between).

## Complexity
- Time: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <queue>

std::vector<std::vector<int>> zigzagLevelOrder(TreeNode* root) {
    if (!root) return {};

    std::vector<std::vector<int>> result;
    std::queue<TreeNode*> q;
    q.push(root);
    bool leftToRight = true;

    while (!q.empty()) {
        int size = q.size();
        std::vector<int> level(size);

        for (int i = 0; i < size; ++i) {
            TreeNode* node = q.front();
            q.pop();

            int index = leftToRight ? i : (size - 1 - i);
            level[index] = node->val;

            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }

        leftToRight = !leftToRight;
        result.push_back(std::move(level));
    }

    return result;
}
```
