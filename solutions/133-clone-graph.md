# Problem 133: Clone Graph

## Problem Statement
Given a reference of a node in a connected undirected graph. Return a deep copy (clone) of the graph.

## Complexity
- Time: $O(V + E)$
- Space: $O(V)$ hash map and call stack

## C++ Implementation
```cpp
#include <vector>
#include <unordered_map>

class Node {
public:
    int val;
    std::vector<Node*> neighbors;
    Node() : val(0) {}
    Node(int _val) : val(_val) {}
};

class Solution {
    std::unordered_map<Node*, Node*> visited;

public:
    Node* cloneGraph(Node* node) {
        if (!node) return nullptr;
        if (visited.count(node)) return visited[node];

        Node* clone = new Node(node->val);
        visited[node] = clone;

        for (Node* neighbor : node->neighbors) {
            clone->neighbors.push_back(cloneGraph(neighbor));
        }
        return clone;
    }
};
```
