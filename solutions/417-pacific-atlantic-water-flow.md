# Problem: Pacific Atlantic Water Flow

## Problem Statement
There is an `m x n` rectangular island that borders both the Pacific Ocean (top and left borders) and Atlantic Ocean (bottom and right borders). Return a 2D list of grid coordinates `result` where `result[i] = [ri, ci]` denotes that rain water can flow from cell `(ri, ci)` to both oceans.

## Intuition & Approach
Reverse Multi-Source Breadth-First Search (BFS):
1. Forward flow (simulating water flowing down from every cell) would require repeated $O(M \times N)$ traversals.
2. Think backwards: simulate water flowing *upwards* from the ocean borders into the island.
3. Queue 1 (`pacific`): Initialize with all cells on top row and left column. Mark visited in `pacific_reachable`.
4. Queue 2 (`atlantic`): Initialize with all cells on bottom row and right column. Mark visited in `atlantic_reachable`.
5. Run BFS expanding to orthogonal neighbours where `height[neighbour] >= height[current]`.
6. Intersect reachable sets: any cell marked true in both matrices can reach both oceans.
7. Time Complexity: $O(M \times N)$. Space Complexity: $O(M \times N)$.

## TypeScript Implementation

```typescript
export function pacificAtlantic(heights: number[][]): number[][] {
  const m = heights.length;
  if (m === 0) return [];
  const n = heights[0].length;
  if (n === 0) return [];

  const pacific: boolean[][] = Array.from({ length: m }, () => new Array(n).fill(false));
  const atlantic: boolean[][] = Array.from({ length: m }, () => new Array(n).fill(false));

  const dirs = [[0, 1], [0, -1], [1, 0], [-1, 0]];

  function bfs(queue: [number, number][], visited: boolean[][]) {
    let head = 0;
    while (head < queue.length) {
      const [r, c] = queue[head++];
      for (const [dr, dc] of dirs) {
        const nr = r + dr;
        const nc = c + dc;
        if (nr >= 0 && nr < m && nc >= 0 && nc < n && !visited[nr][nc]) {
          if (heights[nr][nc] >= heights[r][c]) {
            visited[nr][nc] = true;
            queue.push([nr, nc]);
          }
        }
      }
    }
  }

  const pQueue: [number, number][] = [];
  const aQueue: [number, number][] = [];

  for (let r = 0; r < m; r++) {
    pacific[r][0] = true;
    pQueue.push([r, 0]);
    atlantic[r][n - 1] = true;
    aQueue.push([r, n - 1]);
  }

  for (let c = 0; c < n; c++) {
    pacific[0][c] = true;
    pQueue.push([0, c]);
    atlantic[m - 1][c] = true;
    aQueue.push([m - 1, c]);
  }

  bfs(pQueue, pacific);
  bfs(aQueue, atlantic);

  const results: number[][] = [];
  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      if (pacific[r][c] && atlantic[r][c]) {
        results.push([r, c]);
      }
    }
  }

  return results;
}
```
