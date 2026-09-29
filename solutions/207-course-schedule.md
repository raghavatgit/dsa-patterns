# 207. Course Schedule

## Complexity
- Time Complexity: O(V + E)
- Space Complexity: O(V + E) for adjacency list and indegree table

## Invariant
A directed graph can be topologically sorted if and only if it contains no directed cycles. Kahn algorithm processes nodes with in-degree 0 iteratively.

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn can_finish(num_courses: i32, prerequisites: Vec<Vec<i32>>) -> bool {
    let n = num_courses as usize;
    let mut adj = vec![vec![]; n];
    let mut indegree = vec![0; n];

    for edge in prerequisites {
        let u = edge[1] as usize;
        let v = edge[0] as usize;
        adj[u].push(v);
        indegree[v] += 1;
    }

    let mut q = VecDeque::new();
    for i in 0..n {
        if indegree[i] == 0 { q.push_back(i); }
    }

    let mut visited = 0;
    while let Some(u) = q.pop_front() {
        visited += 1;
        for &v in &adj[u] {
            indegree[v] -= 1;
            if indegree[v] == 0 { q.push_back(v); }
        }
    }

    visited == n
}
```

## TypeScript Implementation
```typescript
export function canFinish(numCourses: number, prerequisites: number[][]): boolean {
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

    let count = 0;
    while (queue.length > 0) {
        const u = queue.shift()!;
        count++;
        for (const v of adj[u]) {
            inDegree[v]--;
            if (inDegree[v] === 0) queue.push(v);
        }
    }

    return count === numCourses;
}
```
