# 684. Redundant Connection

## Complexity
- Time Complexity: O(n * alpha(n))
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn find_redundant_connection(edges: Vec<Vec<i32>>) -> Vec<i32> {
    let n = edges.len();
    let mut parent: Vec<usize> = (0..=n).collect();

    fn find(parent: &mut Vec<usize>, i: usize) -> usize {
        if parent[i] == i { return i; }
        parent[i] = find(parent, parent[i]);
        parent[i]
    }

    for edge in edges {
        let u = edge[0] as usize;
        let v = edge[1] as usize;
        let root_u = find(&mut parent, u);
        let root_v = find(&mut parent, v);
        if root_u == root_v {
            return edge;
        }
        parent[root_u] = root_v;
    }
    vec![]
}
```
