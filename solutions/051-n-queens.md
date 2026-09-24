# Problem 051: N-Queens

## Problem Statement
The n-queens puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other. Return all distinct board configurations.

## Bitmask Backtracking
Track occupied columns, main diagonals (`r - c + n`), and anti-diagonals (`r + c`) using 3 integer bitmasks.

## Complexity
- Time: $O(N!)$
- Space: $O(N)$

## C++ Implementation
```cpp
#include <vector>
#include <string>

class Solution {
    std::vector<std::vector<std::string>> result;
    std::vector<int> queens; // queens[row] = col

    void solve(int row, int n, int cols, int diag1, int diag2) {
        if (row == n) {
            std::vector<std::string> board(n, std::string(n, '.'));
            for (int r = 0; r < n; ++r) {
                board[r][queens[r]] = 'Q';
            }
            result.push_back(board);
            return;
        }

        int available = ((1 << n) - 1) & ~(cols | diag1 | diag2);
        while (available) {
            int p = available & -available;
            available ^= p;
            int col = __builtin_ctz(p);

            queens[row] = col;
            solve(row + 1, n, cols | p, (diag1 | p) << 1, (diag2 | p) >> 1);
        }
    }

public:
    std::vector<std::vector<std::string>> solveNQueens(int n) {
        result.clear();
        queens.resize(n);
        solve(0, n, 0, 0, 0);
        return result;
    }
};
```
