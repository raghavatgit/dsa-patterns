# 994. Rotting Oranges

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(m * n) queue

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn oranges_rotting(mut grid: Vec<Vec<i32>>) -> i32 {
    let m = grid.len();
    let n = grid[0].len();
    let mut queue = VecDeque::new();
    let mut fresh = 0;

    for i in 0..m {
        for j in 0..n {
            if grid[i][j] == 2 { queue.push_back((i, j)); }
            else if grid[i][j] == 1 { fresh += 1; }
        }
    }

    if fresh == 0 { return 0; }
    let mut minutes = 0;
    let dirs = [(-1, 0), (1, 0), (0, -1), (0, 1)];

    while !queue.is_empty() && fresh > 0 {
        let size = queue.len();
        for _ in 0..size {
            let (r, c) = queue.pop_front().unwrap();
            for (dr, dc) in dirs {
                let nr = r as i32 + dr;
                let nc = c as i32 + dc;
                if nr >= 0 && nr < m as i32 && nc >= 0 && nc < n as i32 {
                    let ur = nr as usize;
                    let uc = nc as usize;
                    if grid[ur][uc] == 1 {
                        grid[ur][uc] = 2;
                        fresh -= 1;
                        queue.push_back((ur, uc));
                    }
                }
            }
        }
        minutes += 1;
    }

    if fresh == 0 { minutes } else { -1 }
}
```
