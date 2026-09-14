# Bellman-Ford Shortest Path with Negative Cycle Detection

## Concept
The Bellman-Ford algorithm computes single-source shortest paths in weighted directed graphs, even when negative edge weights are present.

* **Relaxation Principle:** In a graph with `V` vertices without negative weight cycles, any shortest simple path contains at most `V - 1` edges.
* **Algorithm:** Relax all `E` edges `V - 1` times.
* **Negative Cycle Detection:** If any edge can still be relaxed on the `V`-th iteration, a negative cycle exists that allows arbitrarily low path costs.

## Rust Implementation

```rust
#[derive(Copy, Clone, Debug)]
pub struct DirectedEdge {
    pub src: usize,
    pub dest: usize,
    pub weight: i32,
}

pub fn bellman_ford(
    num_vertices: usize,
    edges: &[DirectedEdge],
    source: usize,
) -> Result<Vec<i32>, &'static str> {
    let mut dist = vec![i32::MAX / 2; num_vertices]; // Prevent overflow
    dist[source] = 0;

    // Relax all edges V - 1 times
    for _ in 1..num_vertices {
        for edge in edges {
            if dist[edge.src] + edge.weight < dist[edge.dest] {
                dist[edge.dest] = dist[edge.src] + edge.weight;
            }
        }
    }

    // Check for negative weight cycles on V-th pass
    for edge in edges {
        if dist[edge.src] + edge.weight < dist[edge.dest] {
            return Err("Graph contains a negative weight cycle");
        }
    }

    Ok(dist)
}
```

## Complexity Analysis
* **Time Complexity:** O(V * E) slower than Dijkstra, but works with negative weights.
* **Space Complexity:** O(V) to maintain shortest distances.
