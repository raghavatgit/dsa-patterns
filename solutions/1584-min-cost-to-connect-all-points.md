# Problem 1584: Min Cost to Connect All Points

## Problem Statement
You are given an array `points` representing integer coordinates of some points on a 2D-plane, where `points[i] = [xi, yi]`. Return the minimum cost to make all points connected using Manhattan distance.

## Prim's MST Approach
Maintain minimum distance to unvisited nodes from visited component.
Iterate $N$ times, greedily picking node with smallest cost, then relax all remaining unvisited nodes.

## Complexity
- Time: $O(N^2)$ optimal for dense complete graphs.
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <cmath>
#include <algorithm>
#include <climits>

int minCostConnectPoints(const std::vector<std::vector<int>>& points) {
    int n = points.size();
    std::vector<int> min_dist(n, INT_MAX);
    std::vector<bool> in_mst(n, false);

    min_dist[0] = 0;
    int total_cost = 0;

    for (int step = 0; step < n; ++step) {
        int u = -1;
        for (int i = 0; i < n; ++i) {
            if (!in_mst[i] && (u == -1 || min_dist[i] < min_dist[u])) {
                u = i;
            }
        }

        in_mst[u] = true;
        total_cost += min_dist[u];

        for (int v = 0; v < n; ++v) {
            if (!in_mst[v]) {
                int dist = std::abs(points[u][0] - points[v][0]) + std::abs(points[u][1] - points[v][1]);
                min_dist[v] = std::min(min_dist[v], dist);
            }
        }
    }
    return total_cost;
}
```
