# Problem 785: Is Graph Bipartite?

## Problem Statement
There is an undirected graph with `n` nodes, where each node is numbered between `0` and `n - 1`. A graph is bipartite if the nodes can be partitioned into two independent sets $A$ and $B$ such that every edge connects a node in $A$ and a node in $B$.

## Algorithm
Graph coloring with two colors (1 and -1):
For each connected component, color unvisited starting node with 1.
For all neighbors:
- If neighbor is uncolored, color with opposite color and recurse/enqueue.
- If neighbor has same color, graph is not bipartite.

## Complexity
- Time: $O(V + E)$
- Space: $O(V)$

## C++ Implementation
```cpp
#include <vector>
#include <queue>

bool isBipartite(const std::vector<std::vector<int>>& graph) {
    int n = graph.size();
    std::vector<int> color(n, 0); // 0: uncolored, 1: red, -1: blue

    for (int i = 0; i < n; ++i) {
        if (color[i] != 0) continue;

        std::queue<int> q;
        q.push(i);
        color[i] = 1;

        while (!q.empty()) {
            int u = q.front();
            q.pop();

            for (int v : graph[u]) {
                if (color[v] == 0) {
                    color[v] = -color[u];
                    q.push(v);
                } else if (color[v] == color[u]) {
                    return false;
                }
            }
        }
    }
    return true;
}
```
