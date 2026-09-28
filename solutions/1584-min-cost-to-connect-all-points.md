# 1584. Min Cost to Connect All Points

## Complexity
- Time Complexity: O(V^2)
- Space Complexity: O(V)

## Rust Implementation
```rust
pub fn min_cost_connect_points(points: Vec<Vec<i32>>) -> i32 {
    let n = points.len();
    let mut min_cost = vec![i32::MAX; n];
    let mut visited = vec![false; n];
    min_cost[0] = 0;
    let mut total = 0;

    for _ in 0..n {
        let mut u = None;
        for i in 0..n {
            if !visited[i] && (u.is_none() || min_cost[i] < min_cost[u.unwrap()]) {
                u = Some(i);
            }
        }

        let u = u.unwrap();
        visited[u] = true;
        total += min_cost[u];

        for v in 0..n {
            if !visited[v] {
                let dist = (points[u][0] - points[v][0]).abs() + (points[u][1] - points[v][1]).abs();
                if dist < min_cost[v] {
                    min_cost[v] = dist;
                }
            }
        }
    }

    total
}
```
