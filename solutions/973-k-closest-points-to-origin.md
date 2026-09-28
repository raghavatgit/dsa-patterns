# 973. K Closest Points to Origin

## Complexity
- Time Complexity: O(n log k)
- Space Complexity: O(k)

## Rust Implementation
```rust
use std::collections::BinaryHeap;

#[derive(Eq, PartialEq)]
struct Point {
    dist: i64,
    x: i32,
    y: i32,
}

impl Ord for Point {
    fn cmp(&self, other: &Self) -> std::cmp::Ordering {
        self.dist.cmp(&other.dist)
    }
}

impl PartialOrd for Point {
    fn partial_cmp(&self, other: &Self) -> Option<std::cmp::Ordering> {
        Some(self.cmp(other))
    }
}

pub fn k_closest(points: Vec<Vec<i32>>, k: i32) -> Vec<Vec<i32>> {
    let mut heap = BinaryHeap::new();
    let k = k as usize;

    for p in points {
        let x = p[0];
        let y = p[1];
        let dist = (x as i64) * (x as i64) + (y as i64) * (y as i64);
        heap.push(Point { dist, x, y });
        if heap.len() > k {
            heap.pop();
        }
    }

    heap.into_iter().map(|p| vec![p.x, p.y]).collect()
}
```
