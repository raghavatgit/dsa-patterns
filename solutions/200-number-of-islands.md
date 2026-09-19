# Problem: Number of Islands (Disjoint Set Union)

## Problem Statement
Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

## Intuition & Approach
Disjoint Set Union (Union-Find) with Rank and Path Compression:
1. Map 2D grid coordinates `(r, c)` to 1D identifier: `id = r * n + c`.
2. Count initial land cells `island_count`.
3. Scan grid: when encountering land `'1'`, check right neighbour `(r, c + 1)` and bottom neighbour `(r + 1, c)`.
4. If neighbour is also land, union the two sets. If they were previously in distinct sets, decrement `island_count`.
5. Path compression flattens tree during `find()`, union by rank balances tree height: amortized $O(\alpha(N))$ nearly $O(1)$ per operation.
6. Time Complexity: $O(M \times N \times \alpha(M \times N))$. Space Complexity: $O(M \times N)$ parent array.

## TypeScript Implementation

```typescript
class DSU {
  parent: number[];
  rank: number[];
  count: number;

  constructor(n: number, initialLand: number) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.rank = new Array(n).fill(0);
    this.count = initialLand;
  }

  find(i: number): number {
    if (this.parent[i] === i) return i;
    this.parent[i] = this.find(this.parent[i]);
    return this.parent[i];
  }

  union(i: number, j: number): boolean {
    const rootI = this.find(i);
    const rootJ = this.find(j);
    if (rootI === rootJ) return false;

    if (this.rank[rootI] < this.rank[rootJ]) {
      this.parent[rootI] = rootJ;
    } else if (this.rank[rootI] > this.rank[rootJ]) {
      this.parent[rootJ] = rootI;
    } else {
      this.parent[rootJ] = rootI;
      this.rank[rootI]++;
    }

    this.count--;
    return true;
  }
}

export function numIslands(grid: string[][]): number {
  const m = grid.length;
  if (m === 0) return 0;
  const n = grid[0].length;

  let landCount = 0;
  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      if (grid[r][c] === "1") landCount++;
    }
  }

  const dsu = new DSU(m * n, landCount);

  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      if (grid[r][c] === "1") {
        const id = r * n + c;
        if (r + 1 < m && grid[r + 1][c] === "1") {
          dsu.union(id, (r + 1) * n + c);
        }
        if (c + 1 < n && grid[r][c + 1] === "1") {
          dsu.union(id, r * n + (c + 1));
        }
      }
    }
  }

  return dsu.count;
}
```
