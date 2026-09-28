# 200. Number of Islands

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(m * n) worst case call stack

## Rust Implementation
```rust
pub fn num_islands(mut grid: Vec<Vec<char>>) -> i32 {
    let m = grid.len();
    let n = grid[0].len();
    let mut count = 0;

    fn sink(grid: &mut Vec<Vec<char>>, r: usize, c: usize, m: usize, n: usize) {
        if grid[r][c] != '1' { return; }
        grid[r][c] = '0';

        if r > 0 { sink(grid, r - 1, c, m, n); }
        if r + 1 < m { sink(grid, r + 1, c, m, n); }
        if c > 0 { sink(grid, r, c - 1, m, n); }
        if c + 1 < n { sink(grid, r, c + 1, m, n); }
    }

    for i in 0..m {
        for j in 0..n {
            if grid[i][j] == '1' {
                count += 1;
                sink(&mut grid, i, j, m, n);
            }
        }
    }

    count
}
```

## TypeScript Implementation
```typescript
export function numIslands(grid: string[][]): number {
    const m = grid.length;
    const n = grid[0].length;
    let count = 0;

    const sink = (r: number, c: number) => {
        if (r < 0 || r >= m || c < 0 || c >= n || grid[r][c] !== '1') return;
        grid[r][c] = '0';
        sink(r + 1, c);
        sink(r - 1, c);
        sink(r, c + 1);
        sink(r, c - 1);
    };

    for (let r = 0; r < m; r++) {
        for (let c = 0; c < n; c++) {
            if (grid[r][c] === '1') {
                count++;
                sink(r, c);
            }
        }
    }

    return count;
}
```
