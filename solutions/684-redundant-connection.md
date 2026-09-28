# 684. Redundant Connection

## Complexity
- Time Complexity: O(n * alpha(n))
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn find_redundant_connection(edges: Vec<Vec<i32>>) -> Vec<i32> {
    let n = edges.len() + 1;
    let mut parent: Vec<usize> = (0..n).collect();

    fn find(parent: &mut [usize], mut i: usize) -> usize {
        while i != parent[i] {
            parent[i] = parent[parent[i]];
            i = parent[i];
        }
        i
    }

    for edge in edges {
        let u = find(&mut parent, edge[0] as usize);
        let v = find(&mut parent, edge[1] as usize);
        if u == v {
            return edge;
        }
        parent[u] = v;
    }

    vec![]
}
```
