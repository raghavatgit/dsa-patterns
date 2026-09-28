# 743. Network Delay Time

## Complexity
- Time Complexity: O(E * log V)
- Space Complexity: O(V + E)

## Rust Implementation
```rust
use std::collections::BinaryHeap;
use std::cmp::Ordering;

#[derive(Copy, Clone, Eq, PartialEq)]
struct State {
    cost: i32,
    node: usize,
}

impl Ord for State {
    fn cmp(&self, other: &Self) -> Ordering {
        other.cost.cmp(&self.cost)
    }
}

impl PartialOrd for State {
    fn partial_cmp(&self, other: &Self) -> Option<Ordering> {
        Some(self.cmp(other))
    }
}

pub fn network_delay_time(times: Vec<Vec<i32>>, n: i32, k: i32) -> i32 {
    let n = n as usize;
    let mut adj = vec![Vec::new(); n + 1];
    for t in times {
        adj[t[0] as usize].push((t[1] as usize, t[2]));
    }

    let mut dist = vec![i32::MAX; n + 1];
    let mut heap = BinaryHeap::new();

    dist[k as usize] = 0;
    heap.push(State { cost: 0, node: k as usize });

    while let Some(State { cost, node }) = heap.pop() {
        if cost > dist[node] { continue; }
        for &(next_node, weight) in &adj[node] {
            let next_cost = cost + weight;
            if next_cost < dist[next_node] {
                dist[next_node] = next_cost;
                heap.push(State { cost: next_cost, node: next_node });
            }
        }
    }

    let mut max_delay = 0;
    for i in 1..=n {
        if dist[i] == i32::MAX { return -1; }
        max_delay = std::cmp::max(max_delay, dist[i]);
    }
    max_delay
}
```
