# Problem 207: Course Schedule

## Problem Statement
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`. Return `true` if you can finish all courses.

## Kahn's Algorithm
1. Compute in-degree for all courses.
2. Push all nodes with in-degree 0 to queue.
3. Dequeue node, increment `processed_count`, decrement in-degree of all neighbors.
4. If neighbor in-degree becomes 0, push to queue.
5. Return `processed_count == numCourses`.

## Complexity
- Time: $O(V + E)$
- Space: $O(V + E)$

## C++ Implementation
```cpp
#include <vector>
#include <queue>

bool canFinish(int numCourses, const std::vector<std::vector<int>>& prerequisites) {
    std::vector<std::vector<int>> adj(numCourses);
    std::vector<int> in_degree(numCourses, 0);

    for (const auto& edge : prerequisites) {
        adj[edge[1]].push_back(edge[0]);
        in_degree[edge[0]]++;
    }

    std::queue<int> q;
    for (int i = 0; i < numCourses; ++i) {
        if (in_degree[i] == 0) q.push(i);
    }

    int processed = 0;
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        processed++;

        for (int v : adj[u]) {
            if (--in_degree[v] == 0) {
                q.push(v);
            }
        }
    }
    return processed == numCourses;
}
```
