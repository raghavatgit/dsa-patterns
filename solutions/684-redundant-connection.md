# Problem 684: Redundant Connection

## Problem Statement
In this problem, a tree is an undirected graph that is connected and has no cycles. Return an edge that can be removed so that the resulting graph is a tree of `n` nodes. If there are multiple answers, return the answer that occurs last in the input.

## Approach
Disjoint Set Union (DSU) with path compression and union by rank.
For each edge $(u, v)$:
- If `find(u) == find(v)`, adding this edge creates a cycle. This is the redundant edge.
- Otherwise, `union(u, v)`.

## Complexity
- Time: $O(N \alpha(N))$ where $\alpha$ is the inverse Ackermann function.
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <numeric>

class DSU {
    std::vector<int> parent;
    std::vector<int> rank;
public:
    DSU(int n) : parent(n + 1), rank(n + 1, 0) {
        std::iota(parent.begin(), parent.end(), 0);
    }

    int find(int i) {
        if (parent[i] == i) return i;
        return parent[i] = find(parent[i]);
    }

    bool unite(int i, int j) {
        int root_i = find(i);
        int root_j = find(j);
        if (root_i == root_j) return false;

        if (rank[root_i] < rank[root_j]) {
            parent[root_i] = root_j;
        } else if (rank[root_i] > rank[root_j]) {
            parent[root_j] = root_i;
        } else {
            parent[root_j] = root_i;
            rank[root_i]++;
        }
        return true;
    }
};

class Solution {
public:
    std::vector<int> findRedundantConnection(const std::vector<std::vector<int>>& edges) {
        int n = edges.size();
        DSU dsu(n);
        for (const auto& edge : edges) {
            if (!dsu.unite(edge[0], edge[1])) {
                return edge;
            }
        }
        return {};
    }
};
```
