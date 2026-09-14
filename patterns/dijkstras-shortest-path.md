# Dijkstra's Shortest Path Pattern (Min-Heap Priority Queue)

## Concept
Dijkstra's algorithm finds the shortest path from a single source vertex to all other vertices in a weighted graph with non-negative edge weights.

By maintaining a Min-Heap of `(distance, vertex)`, the algorithm greedily explores the closest unvisited vertex, relaxing distances to its neighbors:
`if dist[u] + weight < dist[v] => dist[v] = dist[u] + weight`.

## TypeScript Implementation

```typescript
export interface Edge {
  to: number;
  weight: number;
}

export function dijkstra(
  numVertices: number,
  adjList: Map<number, Edge[]>,
  source: number
): number[] {
  const dist: number[] = new Array(numVertices).fill(Infinity);
  dist[source] = 0;

  // Min-priority queue: [distance, vertex]
  const pq: [number, number][] = [[0, source]];

  while (pq.length > 0) {
    pq.sort((a, b) => a[0] - b[0]); // Min-heap behavior
    const [d, u] = pq.shift()!;

    if (d > dist[u]) continue; // Stale frontier entry

    const neighbors = adjList.get(u) || [];
    for (const edge of neighbors) {
      const nextDist = dist[u] + edge.weight;
      if (nextDist < dist[edge.to]) {
        dist[edge.to] = nextDist;
        pq.push([nextDist, edge.to]);
      }
    }
  }

  return dist;
}
```

## Rust Implementation

```rust
use std::cmp::Ordering;
use std::collections::BinaryHeap;

#[derive(Copy, Clone, Eq, PartialEq)]
struct State {
    cost: usize,
    position: usize,
}

impl Ord for State {
    fn cmp(&self, other: &Self) -> Ordering {
        // Reverse ordering to transform BinaryHeap (Max-Heap) into Min-Heap
        other.cost.cmp(&self.cost)
    }
}

impl PartialOrd for State {
    fn partial_cmp(&self, other: &Self) -> Option<Ordering> {
        Some(self.cmp(other))
    }
}

pub fn dijkstra(
    num_vertices: usize,
    adj: &[Vec<(usize, usize)>],
    source: usize,
) -> Vec<usize> {
    let mut dist: Vec<usize> = vec![usize::MAX; num_vertices];
    let mut heap = BinaryHeap::new();

    dist[source] = 0;
    heap.push(State { cost: 0, position: source });

    while let Some(State { cost, position }) = heap.pop() {
        if cost > dist[position] {
            continue;
        }

        for &(next_node, weight) in &adj[position] {
            let next_cost = cost + weight;
            if next_cost < dist[next_node] {
                dist[next_node] = next_cost;
                heap.push(State { cost: next_cost, position: next_node });
            }
        }
    }

    dist
}
```

## Complexity Analysis
* **Time Complexity:** O((V + E) log V) with a binary heap priority queue.
* **Space Complexity:** O(V + E) to store the graph and priority queue elements.
