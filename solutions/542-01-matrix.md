# 542. 01 Matrix

## Problem Statement
Given an `m x n` binary matrix `mat`, return the distance of the nearest `0` for each cell.

The distance between two adjacent cells is `1`.

---

## TypeScript Implementation

```typescript
export function updateMatrix(mat: number[][]): number[][] {
  const m = mat.length;
  const n = mat[0].length;
  const dist = Array.from({ length: m }, () => new Array<number>(n).fill(-1));
  const queue: [number, number][] = [];

  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      if (mat[r][c] === 0) {
        dist[r][c] = 0;
        queue.push([r, c]);
      }
    }
  }

  const dirs = [
    [0, 1],
    [1, 0],
    [0, -1],
    [-1, 0],
  ];

  let head = 0;
  while (head < queue.length) {
    const [r, c] = queue[head++];

    for (const [dr, dc] of dirs) {
      const nr = r + dr;
      const nc = c + dc;

      if (nr >= 0 && nr < m && nc >= 0 && nc < n && dist[nr][nc] === -1) {
        dist[nr][nc] = dist[r][c] + 1;
        queue.push([nr, nc]);
      }
    }
  }

  return dist;
}
```

---

## Rust Implementation

```rust
use std::collections::VecDeque;

pub struct Solution;

impl Solution {
    pub fn update_matrix(mat: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        let m = mat.len();
        let n = mat[0].len();
        let mut dist = vec![vec![-1i32; n]; m];
        let mut queue = VecDeque::new();

        for r in 0..m {
            for c in 0..n {
                if mat[r][c] == 0 {
                    dist[r][c] = 0;
                    queue.push_back((r, c));
                }
            }
        }

        let dirs: [(isize, isize); 4] = [(0, 1), (1, 0), (0, -1), (-1, 0)];

        while let Some((r, c)) = queue.pop_front() {
            for (dr, dc) in dirs {
                let nr = r as isize + dr;
                let nc = c as isize + dc;

                if nr >= 0 && nr < m as isize && nc >= 0 && nc < n as isize {
                    let ur = nr as usize;
                    let uc = nc as usize;
                    if dist[ur][uc] == -1 {
                        dist[ur][uc] = dist[r][c] + 1;
                        queue.push_back((ur, uc));
                    }
                }
            }
        }

        dist
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(m * n)` visiting each grid cell once via multi-source BFS.
- Space Complexity: `O(m * n)` for the distance matrix and BFS queue.
