# 452. Minimum Number of Arrows to Burst Balloons

## Complexity
- Time Complexity: O(n log n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn find_min_arrow_shots(mut points: Vec<Vec<i32>>) -> i32 {
    if points.is_empty() { return 0; }
    points.sort_by_key(|p| p[1]);
    let mut arrows = 1;
    let mut end = points[0][1];
    for p in points.iter().skip(1) {
        if p[0] > end {
            arrows += 1;
            end = p[1];
        }
    }
    arrows
}
```

## TypeScript Implementation
```typescript
export function findMinArrowShots(points: number[][]): number {
    if (points.length === 0) return 0;
    points.sort((a, b) => a[1] - b[1]);
    let arrows = 1;
    let end = points[0][1];
    for (let i = 1; i < points.length; i++) {
        if (points[i][0] > end) {
            arrows++;
            end = points[i][1];
        }
    }
    return arrows;
}
```
