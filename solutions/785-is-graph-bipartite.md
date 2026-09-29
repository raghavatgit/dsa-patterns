# 785. Is Graph Bipartite?

## Complexity
- Time Complexity: O(V + E)
- Space Complexity: O(V) color table

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn is_bipartite(graph: Vec<Vec<i32>>) -> bool {
    let n = graph.len();
    let mut colors = vec![0; n]; // 0: unvisited, 1: blue, -1: red

    for i in 0..n {
        if colors[i] != 0 { continue; }
        let mut q = VecDeque::new();
        q.push_back(i);
        colors[i] = 1;

        while let Some(u) = q.pop_front() {
            for &v_i in &graph[u] {
                let v = v_i as usize;
                if colors[v] == 0 {
                    colors[v] = -colors[u];
                    q.push_back(v);
                } else if colors[v] == colors[u] {
                    return false;
                }
            }
        }
    }
    true
}
```
