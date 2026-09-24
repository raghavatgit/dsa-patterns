# Problem 200: Number of Islands

## Problem Statement
Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands.

## Approach
Iterate through matrix. When `'1'` is found, increment island counter and invoke DFS/BFS to mutate connected land to `'0'`.

## Complexity
- Time: $O(M \times N)$
- Space: $O(M \times N)$ recursion stack

## C++ Implementation
```cpp
#include <vector>

class Solution {
    void dfs(std::vector<std::vector<char>>& grid, int r, int c) {
        if (r < 0 || r >= static_cast<int>(grid.size()) ||
            c < 0 || c >= static_cast<int>(grid[0].size()) ||
            grid[r][c] != '1') return;

        grid[r][c] = '0'; // Sink island
        dfs(grid, r + 1, c);
        dfs(grid, r - 1, c);
        dfs(grid, r, c + 1);
        dfs(grid, r, c - 1);
    }

public:
    int numIslands(std::vector<std::vector<char>>& grid) {
        int count = 0;
        for (int r = 0; r < static_cast<int>(grid.size()); ++r) {
            for (int c = 0; c < static_cast<int>(grid[0].size()); ++c) {
                if (grid[r][c] == '1') {
                    count++;
                    dfs(grid, r, c);
                }
            }
        }
        return count;
    }
};
```
