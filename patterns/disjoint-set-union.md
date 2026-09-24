# Pattern: Disjoint Set Union (Union-Find)

## Theoretical Invariants
- **Path Compression**: Flattens tree during `find(x)`, setting parent pointer directly to root: `parent[x] = find(parent[x])`.
- **Union by Rank/Size**: Attaches smaller tree beneath root of larger tree, preventing tree depth deterioration.
- Amortized complexity per operation: $O(\alpha(N))$ where $\alpha$ is the inverse Ackermann function, effectively constant time ($\le 4$) for all practical values.

## Applications
- Connected components in dynamic graphs
- Cycle detection in undirected graphs
- Kruskal's Minimum Spanning Tree algorithm
- Percolation and image segmentation
