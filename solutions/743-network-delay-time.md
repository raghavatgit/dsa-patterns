# Problem 743: Network Delay Time

## Problem Statement
You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (ui, vi, wi)`. Return the minimum time it takes for all the `n` nodes to receive the signal. If it is impossible, return `-1`.

## Algorithm
Dijkstra's Algorithm with Min-Heap Priority Queue.
Relax edges $u \to v$ with weight $w$.
If $\text{dist}[u] + w < \text{dist}[v]$, update and push $(dist[v], v)$.

## Complexity
- Time: $O((V + E) \log V)$
- Space: $O(V + E)$

## C++ Implementation
```cpp
#include <vector>
#include <queue>
#include <algorithm>
#include <climits>

int networkDelayTime(const std::vector<std::vector<int>>& times, int n, int k) {
    std::vector<std::vector<std::pair<int, int>>> adj(n + 1);
    for (const auto& edge : times) {
        adj[edge[0]].push_back({edge[1], edge[2]});
    }

    std::vector<int> dist(n + 1, INT_MAX);
    // {distance, node}
    std::priority_queue<std::pair<int, int>, std::vector<std::pair<int, int>>, std::greater<>> pq;

    dist[k] = 0;
    pq.push({0, k});

    while (!pq.empty()) {
        auto [d, u] = pq.top();
        pq.pop();

        if (d > dist[u]) continue;

        for (const auto& [v, weight] : adj[u]) {
            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }

    int max_time = 0;
    for (int i = 1; i <= n; ++i) {
        if (dist[i] == INT_MAX) return -1;
        max_time = std::max(max_time, dist[i]);
    }
    return max_time;
}
```
