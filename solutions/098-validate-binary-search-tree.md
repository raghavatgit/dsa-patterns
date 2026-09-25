# Problem 098: Validate Binary Search Tree

## Problem Statement
Given the root of a binary tree, determine if it is a valid binary search tree (BST).

## Invariant Formulation
Every node value must satisfy strictly bounded range constraints:
$$low < node\to val < high$$
To handle boundary integer values like `INT_MIN` and `INT_MAX`, use 64-bit integers (`long long`).

## Complexity
- Time: $O(N)$ visit each node once
- Space: $O(H)$ recursion call stack

## C++ Implementation
```cpp
#include <climits>

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
    bool validate(TreeNode* node, long long low, long long high) {
        if (!node) return true;
        if (node->val <= low || node->val >= high) return false;

        return validate(node->left, low, node->val) &&
               validate(node->right, node->val, high);
    }

public:
    bool isValidBST(TreeNode* root) {
        return validate(root, LLONG_MIN, LLONG_MAX);
    }
};
```
