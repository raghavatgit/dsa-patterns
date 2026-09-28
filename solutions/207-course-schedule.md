# 207. Course Schedule

## Complexity
- Time Complexity: O(V + E)
- Space Complexity: O(V + E)

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn can_finish(num_courses: i32, prerequisites: Vec<Vec<i32>>) -> bool {
    let n = num_courses as usize;
    let mut adj = vec![Vec::new(); n];
    let mut in_degree = vec![0; n];

    for edge in prerequisites {
        let course = edge[0] as usize;
        let pre = edge[1] as usize;
        adj[pre].push(course);
        in_degree[course] += 1;
    }

    let mut queue = VecDeque::new();
    for i in 0..n {
        if in_degree[i] == 0 {
            queue.push_back(i);
        }
    }

    let mut visited_count = 0;
    while let Some(u) = queue.pop_front() {
        visited_count += 1;
        for &v in &adj[u] {
            in_degree[v] -= 1;
            if in_degree[v] == 0 {
                queue.push_back(v);
            }
        }
    }

    visited_count == n
}
```

## TypeScript Implementation
```typescript
export function canFinish(numCourses: number, prerequisites: number[][]): boolean {
    const inDegree = new Array(numCourses).fill(0);
    const adj: number[][] = Array.from({ length: numCourses }, () => []);

    for (const [course, pre] of prerequisites) {
        adj[pre].push(course);
        inDegree[course]++;
    }

    const queue: number[] = [];
    for (let i = 0; i < numCourses; i++) {
        if (inDegree[i] === 0) queue.push(i);
    }

    let resolved = 0;
    while (queue.length > 0) {
        const u = queue.shift()!;
        resolved++;
        for (const v of adj[u]) {
            inDegree[v]--;
            if (inDegree[v] === 0) queue.push(v);
        }
    }

    return resolved === numCourses;
}
```
