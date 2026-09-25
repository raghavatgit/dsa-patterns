# Problem 987: Vertical Order Traversal of a Binary Tree

## Problem Statement
Given the root of a binary tree, calculate the vertical order traversal of the binary tree. For each node at `(row, col)`, its left child will be at `(row + 1, col - 1)` and right child at `(row + 1, col + 1)`. Sort primarily by column, secondarily by row, and tertiarily by node value.

## Complexity
- Time: $O(N \log N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <map>
#include <set>
#include <algorithm>

class Solution {
    std::map<int, std::map<int, std::multiset<int>>> nodes;

    void dfs(TreeNode* node, int col, int row) {
        if (!node) return;
        nodes[col][row].insert(node->val);
        dfs(node->left, col - 1, row + 1);
        dfs(node->right, col + 1, row + 1);
    }

public:
    std::vector<std::vector<int>> verticalTraversal(TreeNode* root) {
        nodes.clear();
        dfs(root, 0, 0);

        std::vector<std::vector<int>> result;
        for (auto& [col, rowMap] : nodes) {
            std::vector<int> colVals;
            for (auto& [row, valSet] : rowMap) {
                colVals.insert(colVals.end(), valSet.begin(), valSet.end());
            }
            result.push_back(std::move(colVals));
        }

        return result;
    }
};
```
