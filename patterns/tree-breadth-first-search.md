# Pattern: Tree Breadth-First Search (BFS)

## Invariant Template
```cpp
std::queue<TreeNode*> q;
q.push(root);

while (!q.empty()) {
    int level_size = q.size();
    for (int i = 0; i < level_size; ++i) {
        TreeNode* curr = q.front();
        q.pop();

        if (curr->left) q.push(curr->left);
        if (curr->right) q.push(curr->right);
    }
}
```

## Why BFS?
- Finds shortest path in unweighted graphs/trees.
- Level-by-level evaluation without deep recursion call stack overflow.
