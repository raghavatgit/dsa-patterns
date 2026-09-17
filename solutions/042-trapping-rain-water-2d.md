# Problem: Trapping Rain Water II (2D Elevation Matrix)

## Problem Statement
Given an `m x n` integer matrix `heightMap` representing the height of each unit cell in a 2D elevation map, return the volume of water it can trap after raining.

## Intuition & Approach
Min-Heap Boundary Contraction (Dijkstra-like Flow):
1. Water spilling off the edge can never exceed the lowest boundary bar.
2. Push all boundary cells `(r, c)` of the matrix into a Min-Priority Queue, storing `(height, r, c)` and marking them visited.
3. Keep track of the current maximum water level `water_level = max(water_level, current_cell.height)`.
4. Pop the cell with the minimum height from the heap.
5. Explore its 4-directional unvisited neighbours:
   - If neighbour height is less than `water_level`, it traps `water_level - neighbour_height` units of water.
   - Push neighbour into heap with height `max(neighbour_height, water_level)`.
   - Mark neighbour visited.
6. Time Complexity: $O(M \times N \log(M \times N))$ due to priority queue operations. Space Complexity: $O(M \times N)$ for visited matrix and heap.

## TypeScript Implementation

```typescript
interface Cell {
  r: number;
  c: number;
  h: number;
}

export function trapRainWater(heightMap: number[][]): number {
  const m = heightMap.length;
  if (m === 0) return 0;
  const n = heightMap[0].length;
  if (n === 0) return 0;

  const visited: boolean[][] = Array.from({ length: m }, () => new Array(n).fill(false));
  const heap: Cell[] = [];

  const pushHeap = (cell: Cell) => {
    heap.push(cell);
    let i = heap.length - 1;
    while (i > 0) {
      const p = (i - 1) >> 1;
      if (heap[p].h <= heap[i].h) break;
      const tmp = heap[p];
      heap[p] = heap[i];
      heap[i] = tmp;
      i = p;
    }
  };

  const popHeap = (): Cell => {
    const top = heap[0];
    const last = heap.pop()!;
    if (heap.length > 0) {
      heap[0] = last;
      let i = 0;
      while ((i << 1) + 1 < heap.length) {
        let left = (i << 1) + 1;
        let right = left + 1;
        let best = left;
        if (right < heap.length && heap[right].h < heap[left].h) {
          best = right;
        }
        if (heap[i].h <= heap[best].h) break;
        const tmp = heap[i];
        heap[i] = heap[best];
        heap[best] = tmp;
        i = best;
      }
    }
    return top;
  };

  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      if (r === 0 || r === m - 1 || c === 0 || c === n - 1) {
        pushHeap({ r, c, h: heightMap[r][c] });
        visited[r][c] = true;
      }
    }
  }

  let totalTrapped = 0;
  let currentLevel = 0;
  const dirs = [[0, 1], [0, -1], [1, 0], [-1, 0]];

  while (heap.length > 0) {
    const curr = popHeap();
    currentLevel = Math.max(currentLevel, curr.h);

    for (const [dr, dc] of dirs) {
      const nr = curr.r + dr;
      const nc = curr.c + dc;

      if (nr >= 0 && nr < m && nc >= 0 && nc < n && !visited[nr][nc]) {
        visited[nr][nc] = true;
        if (heightMap[nr][nc] < currentLevel) {
          totalTrapped += currentLevel - heightMap[nr][nc];
        }
        pushHeap({ r: nr, c: nc, h: Math.max(heightMap[nr][nc], currentLevel) });
      }
    }
  }

  return totalTrapped;
}
```

## Rust Implementation

```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;

#[derive(Copy, Clone, Eq, PartialEq)]
struct Cell {
    h: i32,
    r: usize,
    c: usize,
}

impl Ord for Cell {
    fn cmp(&self, other: &Self) -> std::cmp::Ordering {
        self.h.cmp(&other.h)
    }
}

impl PartialOrd for Cell {
    fn partial_cmp(&self, other: &Self) -> Option<std::cmp::Ordering> {
        Some(self.cmp(other))
    }
}

pub fn trap_rain_water(height_map: Vec<Vec<i32>>) -> i32 {
    let m = height_map.len();
    if m == 0 { return 0; }
    let n = height_map[0].len();
    if n == 0 { return 0; }

    let mut visited = vec![vec![false; n]; m];
    let mut heap = BinaryHeap::new();

    for r in 0..m {
        for c in 0..n {
            if r == 0 || r == m - 1 || c == 0 || c == n - 1 {
                heap.push(Reverse(Cell { h: height_map[r][c], r, c }));
                visited[r][c] = true;
            }
        }
    }

    let mut total_trapped = 0;
    let mut water_level = 0;
    let dirs: [(i32, i32); 4] = [(0, 1), (0, -1), (1, 0), (-1, 0)];

    while let Some(Reverse(curr)) = heap.pop() {
        water_level = water_level.max(curr.h);

        for (dr, dc) in dirs {
            let nr = curr.r as i32 + dr;
            let nc = curr.c as i32 + dc;

            if nr >= 0 && nr < m as i32 && nc >= 0 && nc < n as i32 {
                let nr = nr as usize;
                let nc = nc as usize;

                if !visited[nr][nc] {
                    visited[nr][nc] = true;
                    if height_map[nr][nc] < water_level {
                        total_trapped += water_level - height_map[nr][nc];
                    }
                    heap.push(Reverse(Cell {
                        h: height_map[nr][nc].max(water_level),
                        r: nr,
                        c: nc,
                    }));
                }
            }
        }
    }

    total_trapped
}
```
