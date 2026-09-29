# 210. Course Schedule II

## Complexity
- Time Complexity: O(V + E)
- Space Complexity: O(V + E)

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn find_order(num_courses: i32, prerequisites: Vec<Vec<i32>>) -> Vec<i32> {
    let n = num_courses as usize;
    let mut adj = vec![vec![]; n];
    let mut indegree = vec![0; n];

    for edge in prerequisites {
        adj[edge[1] as usize].push(edge[0] as usize);
        indegree[edge[0] as usize] += 1;
    }

    let mut q = VecDeque::new();
    for i in 0..n {
        if indegree[i] == 0 { q.push_back(i); }
    }

    let mut order = Vec::with_capacity(n);
    while let Some(u) = q.pop_front() {
        order.push(u as i32);
        for &v in &adj[u] {
            indegree[v] -= 1;
            if indegree[v] == 0 { q.push_back(v); }
        }
    }

    if order.len() == n { order } else { vec![] }
}
```

## TypeScript Implementation
```typescript
export function findOrder(numCourses: number, prerequisites: number[][]): number[] {
    const adj: number[][] = Array.from({ length: numCourses }, () => []);
    const inDegree: number[] = new Array(numCourses).fill(0);

    for (const [v, u] of prerequisites) {
        adj[u].push(v);
        inDegree[v]++;
    }

    const queue: number[] = [];
    for (let i = 0; i < numCourses; i++) {
        if (inDegree[i] === 0) queue.push(i);
    }

    const order: number[] = [];
    while (queue.length > 0) {
        const u = queue.shift()!;
        order.push(u);
        for (const v of adj[u]) {
            inDegree[v]--;
            if (inDegree[v] === 0) queue.push(v);
        }
    }

    return order.length === numCourses ? order : [];
}
```
