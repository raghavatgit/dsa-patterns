# Pattern: Shortest Path Algorithms Comparison

| Algorithm | Edge Weights | Directed/Undirected | Time Complexity | Space Complexity |
| :--- | :--- | :--- | :--- | :--- |
| BFS | Unweighted ($W=1$) | Both | $O(V + E)$ | $O(V)$ |
| 0-1 BFS | Weights $\in \{0, 1\}$ | Both | $O(V + E)$ | $O(V)$ |
| Dijkstra (Heap) | Non-negative ($W \ge 0$) | Both | $O((V + E) \log V)$ | $O(V + E)$ |
| Bellman-Ford | Arbitrary (detects negative cycle) | Directed | $O(V \times E)$ | $O(V)$ |
| SPFA (Queue BF) | Arbitrary | Directed | $O(E)$ average, $O(V \times E)$ worst | $O(V)$ |
| Floyd-Warshall | All-pairs, no negative cycle | Both | $O(V^3)$ | $O(V^2)$ |
