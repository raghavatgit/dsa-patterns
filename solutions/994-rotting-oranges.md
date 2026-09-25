# 994. Rotting Oranges

## Problem Statement
You are given an `m x n` grid where each cell can have one of three values:
- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten. Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return `-1`.

---

## Method Explanation
Multi-Source Breadth-First Search (BFS):
1. Scan grid: push all coordinates of rotten oranges (`2`) into a queue and count fresh oranges (`1`).
2. If fresh count is `0`, return `0` immediately.
3. Level-order BFS traversal: for each layer of rotten oranges, infect adjacent fresh oranges, decrement fresh count, push newly rotten oranges.
4. Return elapsed minutes if fresh count reaches `0`, otherwise `-1`.

---

## Rust Implementation

```rust
use std::collections::VecDeque;

pub struct Solution;

impl Solution {
    pub fn oranges_rotting(mut grid: Vec<Vec<i32>>) -> i32 {
        let m = grid.len();
        let n = grid[0].len();
        let mut queue = VecDeque::new();
        let mut fresh = 0;

        for r in 0..m {
            for c in 0..n {
                match grid[r][c] {
                    2 => queue.push_back((r, c)),
                    1 => fresh += 1,
                    _ => {}
                }
            }
        }

        if fresh == 0 {
            return 0;
        }

        let dirs = [(0, 1), (0, -1), (1, 0), (-1, 0)];
        let mut minutes = 0;

        while !queue.is_empty() && fresh > 0 {
            let level_size = queue.len();
            for _ in 0..level_size {
                let (r, c) = queue.pop_front().unwrap();

                for (dr, dc) in dirs {
                    let nr = r as i32 + dr;
                    let nc = c as i32 + dc;

                    if nr >= 0 && nr < m as i32 && nc >= 0 && nc < n as i32 {
                        let nr = nr as usize;
                        let nc = nc as usize;

                        if grid[nr][nc] == 1 {
                            grid[nr][nc] = 2;
                            fresh -= 1;
                            queue.push_back((nr, nc));
                        }
                    }
                }
            }
            minutes += 1;
        }

        if fresh == 0 {
            minutes
        } else {
            -1
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_rotting_oranges() {
        assert_eq!(
            Solution::oranges_rotting(vec![
                vec![2, 1, 1],
                vec![1, 1, 0],
                vec![0, 1, 1]
            ]),
            4
        );
        assert_eq!(
            Solution::oranges_rotting(vec![
                vec![2, 1, 1],
                vec![0, 1, 1],
                vec![1, 0, 1]
            ]),
            -1
        );
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(M * N)` since each cell is visited at most once.
- Space Complexity: `O(M * N)` for the queue in worst-case grid saturation.
