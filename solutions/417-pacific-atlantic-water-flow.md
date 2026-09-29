# 417. Pacific Atlantic Water Flow

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(m * n)

## Rust Implementation
```rust
pub fn pacific_atlantic(heights: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
    let m = heights.len();
    let n = heights[0].len();
    let mut pac = vec![vec![false; n]; m];
    let mut atl = vec![vec![false; n]; m];

    fn dfs(h: &Vec<Vec<i32>>, r: usize, c: usize, visited: &mut Vec<Vec<bool>>, m: usize, n: usize) {
        visited[r][c] = true;
        let dirs = [(-1, 0), (1, 0), (0, -1), (0, 1)];
        for (dr, dc) in dirs {
            let nr = r as i32 + dr;
            let nc = c as i32 + dc;
            if nr >= 0 && nr < m as i32 && nc >= 0 && nc < n as i32 {
                let ur = nr as usize;
                let uc = nc as usize;
                if !visited[ur][uc] && h[ur][uc] >= h[r][c] {
                    dfs(h, ur, uc, visited, m, n);
                }
            }
        }
    }

    for i in 0..m {
        dfs(&heights, i, 0, &mut pac, m, n);
        dfs(&heights, i, n - 1, &mut atl, m, n);
    }
    for j in 0..n {
        dfs(&heights, 0, j, &mut pac, m, n);
        dfs(&heights, m - 1, j, &mut atl, m, n);
    }

    let mut res = Vec::new();
    for i in 0..m {
        for j in 0..n {
            if pac[i][j] && atl[i][j] {
                res.push(vec![i as i32, j as i32]);
            }
        }
    }
    res
}
```
