# Problem 297: Serialize and Deserialize Binary Tree

## Problem Statement
Design an algorithm to serialize and deserialize a binary tree.

## Approach
Preorder traversal with sentinel `#` for null pointers.
- Serialization: Preorder DFS outputting comma-separated values.
- Deserialization: Tokenize stream, recursively reconstruct left and right subtrees.

## Complexity
- Time: $O(N)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <string>
#include <sstream>

class Codec {
    void serializeDFS(TreeNode* root, std::ostringstream& out) {
        if (!root) {
            out << "#,";
            return;
        }
        out << root->val << ",";
        serializeDFS(root->left, out);
        serializeDFS(root->right, out);
    }

    TreeNode* deserializeDFS(std::istringstream& in) {
        std::string val;
        if (!std::getline(in, val, ',')) return nullptr;
        if (val == "#") return nullptr;

        TreeNode* node = new TreeNode(std::stoi(val));
        node->left = deserializeDFS(in);
        node->right = deserializeDFS(in);
        return node;
    }

public:
    std::string serialize(TreeNode* root) {
        std::ostringstream out;
        serializeDFS(root, out);
        return out.str();
    }

    TreeNode* deserialize(const std::string& data) {
        std::istringstream in(data);
        return deserializeDFS(in);
    }
};
```
