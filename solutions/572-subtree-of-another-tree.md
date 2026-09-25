# Problem 572: Subtree of Another Tree

## Problem Statement
Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

## Algorithm
- `isSame(p, q)` checks structural and value identity.
- Recurse: `isSame(root, subRoot) || isSubtree(root->left, subRoot) || isSubtree(root->right, subRoot)`.

## Complexity
- Time: $O(M \times N)$
- Space: $O(H)$

## C++ Implementation
```cpp
class Solution {
    bool isSame(TreeNode* s, TreeNode* t) {
        if (!s && !t) return true;
        if (!s || !t) return false;
        if (s->val != t->val) return false;
        return isSame(s->left, t->left) && isSame(s->right, t->right);
    }

public:
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if (!root) return false;
        if (isSame(root, subRoot)) return true;
        return isSubtree(root->left, subRoot) || isSubtree(root->right, subRoot);
    }
};
```
