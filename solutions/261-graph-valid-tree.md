# 261. Graph Valid Tree

## Complexity
- Time Complexity: O(V * alpha(V))
- Space Complexity: O(V)

## Rust Implementation
```rust
pub fn valid_tree(n: i32, edges: Vec<Vec<i32>>) -> bool {
    if edges.len() != (n - 1) as usize {
        return false;
    }

    let mut parent: Vec<usize> = (0..n as usize).collect();

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
            return false;
        }
        parent[u] = v;
    }

    true
}
```
