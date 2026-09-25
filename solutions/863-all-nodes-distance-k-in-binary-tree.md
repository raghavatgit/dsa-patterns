# Problem 863: All Nodes Distance K in Binary Tree

## Problem Statement
Given the root of a binary tree, the value of a target node `target`, and an integer `k`, return an array of the values of all nodes that have a distance `k` from the target node.

## Graph Conversion and BFS
1. Build parent pointers map using DFS traversal.
2. Treat tree as an undirected graph.
3. Execute BFS originating at `target` node up to distance $K$.

## Complexity
- Time: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <unordered_map>
#include <unordered_set>
#include <queue>

class Solution {
    std::unordered_map<TreeNode*, TreeNode*> parentMap;

    void mapParents(TreeNode* node, TreeNode* parent) {
        if (!node) return;
        parentMap[node] = parent;
        mapParents(node->left, node);
        mapParents(node->right, node);
    }

public:
    std::vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        mapParents(root, nullptr);

        std::queue<TreeNode*> q;
        std::unordered_set<TreeNode*> visited;
        q.push(target);
        visited.insert(target);

        int currentDistance = 0;
        while (!q.empty()) {
            if (currentDistance == k) {
                std::vector<int> result;
                while (!q.empty()) {
                    result.push_back(q.front()->val);
                    q.pop();
                }
                return result;
            }

            int size = q.size();
            for (int i = 0; i < size; ++i) {
                TreeNode* curr = q.front();
                q.pop();

                if (curr->left && !visited.count(curr->left)) {
                    visited.insert(curr->left);
                    q.push(curr->left);
                }
                if (curr->right && !visited.count(curr->right)) {
                    visited.insert(curr->right);
                    q.push(curr->right);
                }
                if (parentMap[curr] && !visited.count(parentMap[curr])) {
                    visited.insert(parentMap[curr]);
                    q.push(parentMap[curr]);
                }
            }
            currentDistance++;
        }

        return {};
    }
};
```
