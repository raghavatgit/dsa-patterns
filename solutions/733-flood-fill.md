# 733. Flood Fill

## Problem Statement
An image is represented by an `m x n` integer grid `image` where `image[i][j]` represents the pixel value of the image.

You are also given three integers `sr`, `sc`, and `color`. You should perform a **flood fill** on the image starting from the pixel `image[sr][sc]`.

To perform a flood fill, consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with `color`.

Return the modified image after performing the flood fill.

---

## TypeScript Implementation

```typescript
export function floodFill(image: number[][], sr: number, sc: number, color: number): number[][] {
  const origColor = image[sr][sc];
  if (origColor === color) return image;

  const m = image.length;
  const n = image[0].length;

  function dfs(r: number, c: number): void {
    if (r < 0 || r >= m || c < 0 || c >= n || image[r][c] !== origColor) {
      return;
    }

    image[r][c] = color;
    dfs(r + 1, c);
    dfs(r - 1, c);
    dfs(r, c + 1);
    dfs(r, c - 1);
  }

  dfs(sr, sc);
  return image;
}
```

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn flood_fill(mut image: Vec<Vec<i32>>, sr: i32, sc: i32, color: i32) -> Vec<Vec<i32>> {
        let r = sr as usize;
        let c = sc as usize;
        let orig = image[r][c];

        if orig == color {
            return image;
        }

        let m = image.len();
        let n = image[0].len();
        Self::dfs(&mut image, r, c, orig, color, m, n);
        image
    }

    fn dfs(img: &mut Vec<Vec<i32>>, r: usize, c: usize, orig: i32, target: i32, m: usize, n: usize) {
        if img[r][c] != orig {
            return;
        }

        img[r][c] = target;

        let dirs: [(isize, isize); 4] = [(0, 1), (1, 0), (0, -1), (-1, 0)];
        for (dr, dc) in dirs {
            let nr = r as isize + dr;
            let nc = c as isize + dc;
            if nr >= 0 && nr < m as isize && nc >= 0 && nc < n as isize {
                Self::dfs(img, nr as usize, nc as usize, orig, target, m, n);
            }
        }
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(m * n)` each pixel is visited at most once.
- Space Complexity: `O(m * n)` worst-case call stack recursion depth.
