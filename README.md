# Data Structures and Algorithmic Patterns

A collection of foundational algorithmic patterns, time-complexity analyses, and clean implementations in Rust and TypeScript.

---

## Pattern Matrix

| Pattern | Primary Use Cases | Time Complexity | Implementations |
| :--- | :--- | :--- | :--- |
| **Sliding Window** | Subarray / Substring limits, running averages | O(N) | [TypeScript / Rust](patterns/sliding-window.md) |
| **Two Pointers** | Sorted arrays, pair sums, palindrome verification | O(N) | [TypeScript / Rust](patterns/two-pointers.md) |
| **Binary Search** | Monotonic search spaces, range boundaries | O(log N) | [TypeScript / Rust](patterns/binary-search.md) |
| **Fast & Slow Pointers** | Cycle detection in lists/arrays, midpoint lookups | O(N) | [TypeScript / Rust](patterns/fast-slow-pointers.md) |
| **Monotonic Stack** | Next greater element, histogram areas, temperatures | O(N) | [TypeScript / Rust](patterns/monotonic-stack.md) |
| **Prefix Sums** | Static range sum queries, cumulative balances | O(1) query | [TypeScript / Rust](patterns/prefix-sums.md) |
| **Kadane's Algorithm** | Maximum contiguous subarray sum | O(N) | [TypeScript / Rust](patterns/kadanes-algorithm.md) |
| **Binary Tree Traversals** | Hierarchical serialization, level orders | O(N) | [TypeScript / Rust](patterns/binary-tree-traversals.md) |
| **Trie (Prefix Tree)** | Autocomplete dictionaries, prefix matching | O(L) | [TypeScript / Rust](patterns/trie-prefix-tree.md) |
| **LRU Cache** | Fixed-capacity recency cache eviction | O(1) get/put | [TypeScript / Rust](patterns/lru-cache.md) |
| **Topological Sort** | Dependency resolution, build DAG ordering | O(V + E) | [TypeScript / Rust](patterns/topological-sort.md) |
| **Interval Merging** | Calendar scheduling, range consolidation | O(N log N) | [TypeScript / Rust](patterns/interval-merging.md) |

| **2D Flood Fill & BFS** | Grid traversal, connected components, shortest path | O(M * N) | [TypeScript / Rust](patterns/matrix-dfs-bfs-flood-fill.md) |
| **Disjoint Set Union** | Dynamic connectivity, Kruskal MST, cycle checks | O(alpha(N)) | [TypeScript / Rust](patterns/disjoint-set-union.md) |

| **Connected Components** | Graph reachability, island isolation, component IDs | O(V + E) | [C / TypeScript / Rust](patterns/connected-components-undirected-graph.md) |
| **Dijkstra's Algorithm** | Single-source shortest path with non-negative weights | O((V + E) log V) | [TypeScript / Rust](patterns/dijkstras-shortest-path.md) |

| **BFS Shortest Hop** | Unweighted shortest path, hop counts, level orders | O(V + E) | [C / TypeScript / Rust](patterns/bfs-unweighted-shortest-path.md) |
| **Bellman-Ford** | Negative weights, negative cycle detection | O(V * E) | [TypeScript / Rust](patterns/bellman-ford-algorithm.md) |

---

## Solved Problems Catalog

In addition to abstract patterns, explore concrete, fully tested problem writeups in the [Solutions Archive](solutions/):
* [Two Sum (Hash Map)](solutions/001-two-sum.md)
* [Three Sum (Two Pointers)](solutions/015-three-sum.md)
* [Trapping Rain Water (Two Pointers)](solutions/042-trapping-rain-water.md)
* [Maximum Subarray (Kadane)](solutions/053-maximum-subarray.md)
* [Minimum Window Substring (Sliding Window)](solutions/076-minimum-window-substring.md)
* [Number of Islands (Grid Traversal)](solutions/200-number-of-islands.md)
* [Course Schedule (Topological Sort / DAG)](solutions/207-course-schedule.md)
