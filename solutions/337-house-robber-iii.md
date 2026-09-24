# Problem 337: House Robber III

## Problem Statement
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called root. Aside from the root, each house has one and only one parent house. Determine the maximum amount of money the thief can rob without alerting the police.

## Tree DP Formulation
For each node, compute a pair `(rob_this, not_rob_this)`:
- `rob_this = node->val + left.not_rob + right.not_rob`
- `not_rob_this = max(left.rob, left.not_rob) + max(right.rob, right.not_rob)`

## Complexity
- Time: $O(N)$ visit each node once.
- Space: $O(H)$ recursion call stack.

## C++ Implementation
```cpp
#include <algorithm>
#include <utility>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
    std::pair<int, int> dfs(TreeNode* root) {
        if (!root) return {0, 0};

        auto left = dfs(root->left);
        auto right = dfs(root->right);

        int rob_curr = root->val + left.second + right.second;
        int not_rob_curr = std::max(left.first, left.second) + std::max(right.first, right.second);

        return {rob_curr, not_rob_curr};
    }

public:
    int rob(TreeNode* root) {
        auto res = dfs(root);
        return std::max(res.first, res.second);
    }
};
```
