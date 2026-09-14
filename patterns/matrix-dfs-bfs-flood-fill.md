# 2D Matrix Flood Fill and BFS Traversal Pattern

## Concept
Grid traversal algorithms model a 2D matrix as an implicit graph where each coordinate `(r, c)` has up to four orthogonal neighbors:
`[(r - 1, c), (r + 1, c), (r, c - 1), (r, c + 1)]`.

* **Flood Fill / Island Traversal:** Explores connected regions using DFS or BFS.
* **Shortest Path in Grids:** Computed using BFS queue levels to guarantee minimum step traversal.

## TypeScript Implementation

```typescript
export function floodFill(
  image: number[][],
  sr: number,
  sc: number,
  newColor: number
): number[][] {
  const originalColor = image[sr][sc];
  if (originalColor === newColor) return image;

  const rows = image.length;
  const cols = image[0].length;
  const queue: [number, number][] = [[sr, sc]];
  image[sr][sc] = newColor;

  const directions: [number, number][] = [
    [-1, 0], // Up
    [1, 0],  // Down
    [0, -1], // Left
    [0, 1]   // Right
  ];

  while (queue.length > 0) {
    const [r, c] = queue.shift()!;

    for (const [dr, dc] of directions) {
      const nr = r + dr;
      const nc = c + dc;

      // Coordinate boundary and color guard
      if (
        nr >= 0 &&
        nr < rows &&
        nc >= 0 &&
        nc < cols &&
        image[nr][nc] === originalColor
      ) {
        image[nr][nc] = newColor;
        queue.push([nr, nc]);
      }
    }
  }

  return image;
}
```

## Rust Implementation

```rust
use std::collections::VecDeque;

pub fn flood_fill(
    mut image: Vec<Vec<i32>>,
    sr: usize,
    sc: usize,
    new_color: i32,
) -> Vec<Vec<i32>> {
    let original_color = image[sr][sc];
    if original_color == new_color {
        return image;
    }

    let rows = image.len();
    let cols = image[0].len();
    let mut queue = VecDeque::new();
    
    image[sr][sc] = new_color;
    queue.push_back((sr, sc));

    let directions: [(isize, isize); 4] = [(-1, 0), (1, 0), (0, -1), (0, 1)];

    while let Some((r, c)) = queue.pop_front() {
        for &(dr, dc) in &directions {
            let nr = r as isize + dr;
            let nc = c as isize + dc;

            if nr >= 0 && nr < rows as isize && nc >= 0 && nc < cols as isize {
                let ur = nr as usize;
                let uc = nc as usize;

                if image[ur][uc] == original_color {
                    image[ur][uc] = new_color;
                    queue.push_back((ur, uc));
                }
            }
        }
    }

    image
}
```

## Complexity Analysis
* **Time Complexity:** O(M * N) where M is rows and N is columns. Every grid cell is enqueued and recolored at most once.
* **Space Complexity:** O(M * N) worst case queue buffer for complete matrix saturation.
