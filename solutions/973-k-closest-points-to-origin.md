# 973. K Closest Points to Origin

## Problem Statement
Given an array of `points` where `points[i] = [xi, yi]` represents a point on the X-Y plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

The distance between two points on the X-Y plane is the Euclidean distance (`sqrt((x1 - x2)^2 + (y1 - y2)^2)`).

You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).

---

## TypeScript Implementation

```typescript
export function kClosest(points: number[][], k: number): number[][] {
  const dist = (p: number[]) => p[0] * p[0] + p[1] * p[1];
  
  // Quickselect partitioning approach for O(n) average time
  let left = 0;
  let right = points.length - 1;

  while (left <= right) {
    const pivotIdx = partition(points, left, right, dist);
    if (pivotIdx === k) {
      break;
    } else if (pivotIdx < k) {
      left = pivotIdx + 1;
    } else {
      right = pivotIdx - 1;
    }
  }

  return points.slice(0, k);
}

function partition(
  arr: number[][],
  low: number,
  high: number,
  dist: (p: number[]) => number
): number {
  const pivotDist = dist(arr[high]);
  let i = low;

  for (let j = low; j < high; j++) {
    if (dist(arr[j]) <= pivotDist) {
      [arr[i], arr[j]] = [arr[j], arr[i]];
      i++;
    }
  }
  [arr[i], arr[high]] = [arr[high], arr[i]];
  return i;
}
```

---

## Rust Implementation

```rust
use std::collections::BinaryHeap;

#[derive(Eq, PartialEq)]
struct PointEntry {
    dist: i64,
    x: i32,
    y: i32,
}

impl Ord for PointEntry {
    fn cmp(&self, other: &Self) -> std::cmp::Ordering {
        self.dist.cmp(&other.dist)
    }
}

impl PartialOrd for PointEntry {
    fn partial_cmp(&self, other: &Self) -> Option<std::cmp::Ordering> {
        Some(self.cmp(other))
    }
}

pub struct Solution;

impl Solution {
    pub fn k_closest(points: Vec<Vec<i32>>, k: i32) -> Vec<Vec<i32>> {
        let k_usize = k as usize;
        let mut heap: BinaryHeap<PointEntry> = BinaryHeap::with_capacity(k_usize + 1);

        for p in points {
            let (x, y) = (p[0], p[1]);
            let dist = (x as i64) * (x as i64) + (y as i64) * (y as i64);
            heap.push(PointEntry { dist, x, y });

            if heap.len() > k_usize {
                heap.pop();
            }
        }

        heap.into_iter().map(|item| vec![item.x, item.y]).collect()
    }
}
```

---

## Complexity Analysis

- Time Complexity:
  - Max-Heap: `O(n log k)` worst-case.
  - Quickselect: `O(n)` average, `O(n^2)` worst-case.
- Space Complexity: `O(k)` heap storage.
