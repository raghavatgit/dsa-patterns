# Problem 662: Maximum Width of Binary Tree

## Problem Statement
Given the root of a binary tree, return the maximum width of the given tree. The maximum width of a tree is the maximum width among all levels. Width is the length between end-nodes (the leftmost and rightmost non-null nodes).

## 64-Bit Index Normalization
Label nodes as binary heap indices: left child $2i$, right child $2i + 1$.
To prevent integer overflow on skewed trees, subtract the minimum index of each level from all indices in that level:
`normalized_index = index - level_min`.

## Complexity
- Time: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <queue>
#include <algorithm>

int widthOfBinaryTree(TreeNode* root) {
    if (!root) return 0;

    unsigned long long maxWidth = 0;
    std::queue<std::pair<TreeNode*, unsigned long long>> q;
    q.push({root, 0});

    while (!q.empty()) {
        int size = q.size();
        unsigned long long minIdx = q.front().second;
        unsigned long long first = 0, last = 0;

        for (int i = 0; i < size; ++i) {
            auto [node, idx] = q.front();
            q.pop();

            unsigned long long currIdx = idx - minIdx;
            if (i == 0) first = currIdx;
            if (i == size - 1) last = currIdx;

            if (node->left) q.push({node->left, 2 * currIdx + 1});
            if (node->right) q.push({node->right, 2 * currIdx + 2});
        }

        maxWidth = std::max(maxWidth, last - first + 1);
    }

    return static_cast<int>(maxWidth);
}
```
