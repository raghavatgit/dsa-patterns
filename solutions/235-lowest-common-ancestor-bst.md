# Problem 235: Lowest Common Ancestor of a Binary Search Tree

## Problem Statement
Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes `p` and `q`.

## BST Invariant Approach
- If both `p->val` and `q->val` are strictly less than `root->val`, LCA lies in left subtree.
- If both are strictly greater than `root->val`, LCA lies in right subtree.
- Otherwise, `root` is the split point and therefore the LCA.

## Complexity
- Time: $O(H)$ where $H$ is tree height ($O(\log N)$ balanced).
- Space: $O(1)$ iterative.

## C++ Implementation
```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    TreeNode* curr = root;
    while (curr) {
        if (p->val < curr->val && q->val < curr->val) {
            curr = curr->left;
        } else if (p->val > curr->val && q->val > curr->val) {
            curr = curr->right;
        } else {
            return curr;
        }
    }
    return nullptr;
}
```
