# Solved Problem Directory

Production-grade, verified algorithmic problem solutions implemented in Rust and TypeScript with formal complexity analyses, edge cases, and unit tests.

| ID | Title | Pattern / Category | Difficulty | Optimal Time | Space |
|---|---|---|---|---|---|
| 001 | Two Sum | Hash Map Indexing | Easy | $O(N)$ | $O(N)$ |
| 003 | Longest Substring Without Repeating Characters | Sliding Window | Medium | $O(N)$ | $O(\min(N, \Sigma))$ |
| 004 | Median of Two Sorted Arrays | Binary Search Partition | Hard | $O(\log(\min(M, N)))$ | $O(1)$ |
| 010 | Regular Expression Matching | 2D Dynamic Programming | Hard | $O(MN)$ | $O(MN)$ |
| 011 | Container With Most Water | Two Pointers | Medium | $O(N)$ | $O(1)$ |
| 015 | 3Sum | Two Pointers & Pruning | Medium | $O(N^2)$ | $O(1)$ |
| 017 | Letter Combinations of a Phone Number | Cartesian Product BFS | Medium | $O(4^N N)$ | $O(4^N N)$ |
| 020 | Valid Parentheses | Stack LIFO Invariants | Easy | $O(N)$ | $O(N)$ |
| 022 | Generate Parentheses | Balanced Bracket Backtracking | Medium | $O(4^n / \sqrt{n})$ | $O(N)$ |
| 023 | Merge k Sorted Lists | Min-Heap Priority Queue | Hard | $O(N \log k)$ | $O(k)$ |
| 025 | Reverse Nodes in k-Group | Iterative Pointer Reversal | Hard | $O(N)$ | $O(1)$ |
| 032 | Longest Valid Parentheses | Two-Pass Counter Scan | Hard | $O(N)$ | $O(1)$ |
| 033 | Search in Rotated Sorted Array | Modified Binary Search | Medium | $O(\log N)$ | $O(1)$ |
| 034 | Find First and Last Position | Dual Binary Search | Medium | $O(\log N)$ | $O(1)$ |
| 039 | Combination Sum | Unbounded Candidate Backtracking | Medium | $O(N^{T / \min C})$ | $O(T / \min C)$ |
| 040 | Combination Sum II | Bounded Sibling Deduplication | Medium | $O(2^N)$ | $O(N)$ |
| 041 | First Missing Positive | In-Place Cyclic Sort | Hard | $O(N)$ | $O(1)$ |
| 042 | Trapping Rain Water II | Min-Heap Boundary Flow | Hard | $O(MN \log(MN))$ | $O(MN)$ |
| 044 | Wildcard Matching | Greedy Star Checkpoint | Hard | $O(N)$ avg | $O(1)$ |
| 045 | Jump Game II | Greedy Range BFS | Medium | $O(N)$ | $O(1)$ |
| 046 | Permutations | In-Place Swap Backtracking | Medium | $O(N \times N!)$ | $O(N)$ |
| 047 | Permutations II | Used Flags Sibling Pruning | Medium | $O(N \times N!)$ | $O(N)$ |
| 051 | N-Queens | Bitmask Backtracking | Hard | $O(N!)$ | $O(N)$ |
| 053 | Maximum Subarray | Kadane's Algorithm | Medium | $O(N)$ | $O(1)$ |
| 055 | Jump Game | Greedy Boundary | Medium | $O(N)$ | $O(1)$ |
| 062 | Unique Paths | Combinatorics Closed-Form | Medium | $O(\min(M, N))$ | $O(1)$ |
| 064 | Minimum Path Sum | 1D Rolling Array DP | Medium | $O(MN)$ | $O(N)$ |
| 069 | Sqrt(x) | Integer Binary Search | Easy | $O(\log X)$ | $O(1)$ |
| 070 | Climbing Stairs | Fibonacci Recurrence | Easy | $O(N)$ | $O(1)$ |
| 072 | Edit Distance | 1D Rolling DP | Hard | $O(MN)$ | $O(N)$ |
| 074 | Search a 2D Matrix | Virtual 1D Binary Search | Medium | $O(\log(MN))$ | $O(1)$ |
| 076 | Minimum Window Substring | Sliding Window | Hard | $O(M + N)$ | $O(K)$ |
| 078 | Subsets | Cascading Backtracking | Medium | $O(N 2^N)$ | $O(N)$ |
| 079 | Word Search | In-Place Grid Flipping DFS | Medium | $O(MN 3^L)$ | $O(L)$ |
| 084 | Largest Rectangle in Histogram | Monotonic Stack | Hard | $O(N)$ | $O(N)$ |
| 090 | Subsets II | Duplicate Sibling Pruning | Medium | $O(N 2^N)$ | $O(N)$ |
| 091 | Decode Ways | Space-Optimized DP | Medium | $O(N)$ | $O(1)$ |
| 098 | Validate Binary Search Tree | Min/Max Range Bounds | Medium | $O(N)$ | $O(H)$ |
| 104 | Maximum Depth of Binary Tree | Post-Order DFS | Easy | $O(N)$ | $O(H)$ |
| 121 | Best Time to Buy and Sell Stock | Kadane's Accumulator | Easy | $O(N)$ | $O(1)$ |
| 124 | Binary Tree Maximum Path Sum | Post-Order Tree DP | Hard | $O(N)$ | $O(H)$ |
| 127 | Word Ladder | Bidirectional BFS | Hard | $O(M^2 N)$ | $O(MN)$ |
| 128 | Longest Consecutive Sequence | Hash Set Root Scan | Medium | $O(N)$ | $O(N)$ |
| 133 | Clone Graph | DFS Pointer Memoization | Medium | $O(V + E)$ | $O(V)$ |
| 139 | Word Break | Prefix Partitioning DP | Medium | $O(N^2)$ | $O(N)$ |
| 146 | LRU Cache | Doubly Linked List + Map | Medium | $O(1)$ | $O(C)$ |
| 152 | Maximum Product Subarray | Dual Min/Max DP | Medium | $O(N)$ | $O(1)$ |
| 153 | Find Min in Rotated Sorted Array | Binary Search Inflection | Medium | $O(\log N)$ | $O(1)$ |
| 155 | Min Stack | Paired Value/Min Stack | Medium | $O(1)$ | $O(N)$ |
| 162 | Find Peak Element | Binary Search Gradient | Medium | $O(\log N)$ | $O(1)$ |
| 169 | Majority Element | Boyer-Moore Majority Voting | Easy | $O(N)$ | $O(1)$ |
| 198 | House Robber | Space-Optimized DP | Medium | $O(N)$ | $O(1)$ |
| 200 | Number of Islands | Disjoint Set Union | Medium | $O(MN \alpha(MN))$ | $O(MN)$ |
| 206 | Reverse Linked List | Iterative Pointer Swap | Easy | $O(N)$ | $O(1)$ |
| 207 | Course Schedule | Kahn's Topological Sort | Medium | $O(V + E)$ | $O(V + E)$ |
| 208 | Implement Trie (Prefix Tree) | Array-Backed 26-Way Tree | Medium | $O(L)$ | $O(\Sigma NL)$ |
| 212 | Word Search II | Trie 2D Backtracking | Hard | $O(MN 4^L)$ | $O(\Sigma L)$ |
| 218 | The Skyline Problem | Critical Point Line Sweep | Hard | $O(N \log N)$ | $O(N)$ |
| 226 | Invert Binary Tree | Recursive Child Swap | Easy | $O(N)$ | $O(H)$ |
| 229 | Majority Element II | Generalized Boyer-Moore | Medium | $O(N)$ | $O(1)$ |
| 236 | Lowest Common Ancestor | Post-Order Tree Search | Medium | $O(N)$ | $O(H)$ |
| 238 | Product of Array Except Self | Prefix/Suffix Accumulators | Medium | $O(N)$ | $O(1)$ |
| 239 | Sliding Window Maximum | Monotonic Decreasing Deque | Hard | $O(N)$ | $O(K)$ |
| 240 | Search a 2D Matrix II | Top-Right Corner Elimination | Medium | $O(M + N)$ | $O(1)$ |
| 295 | Find Median from Data Stream | Dual Heaps Balancing | Hard | $O(\log N)$ | $O(N)$ |
| 297 | Serialize and Deserialize Binary Tree | Pre-Order String Tokens | Hard | $O(N)$ | $O(N)$ |
| 300 | Longest Increasing Subsequence | Patience Binary Search | Medium | $O(N \log N)$ | $O(N)$ |
| 307 | Range Sum Query Mutable | Fenwick Tree / BIT | Medium | $O(\log N)$ | $O(N)$ |
| 312 | Burst Balloons | Reverse Interval DP | Hard | $O(N^3)$ | $O(N^2)$ |
| 315 | Count of Smaller Numbers After Self | Modified Merge Sort | Hard | $O(N \log N)$ | $O(N)$ |
| 322 | Coin Change | Unbounded Knapsack DP | Medium | $O(N \times \text{amt})$ | $O(\text{amt})$ |
| 329 | Longest Increasing Path in Matrix | Memoized DAG DFS | Hard | $O(MN)$ | $O(MN)$ |
| 417 | Pacific Atlantic Water Flow | Multi-Source Reverse BFS | Medium | $O(MN)$ | $O(MN)$ |
| 543 | Diameter of Binary Tree | Post-Order Depth DFS | Easy | $O(N)$ | $O(H)$ |
| 875 | Koko Eating Bananas | Monotonic Binary Search | Medium | $O(N \log(\max P))$ | $O(1)$ |
