# Problem: Course Schedule (Kahn's Topological Sort)

## Problem Statement
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [a, b]` indicates that you must take course `b` first if you want to take course `a`. Return `true` if you can finish all courses, or `false` if a circular dependency exists.

## Intuition & Approach
Kahn's In-Degree BFS Algorithm:
1. Build adjacency list representation of the directed graph and calculate in-degree (number of prerequisites) for every course.
2. Initialize a queue with all vertices having an in-degree of 0 (no prerequisites needed).
3. Dequeue a vertex, increment processed count, and decrement in-degree of all its directed neighbours.
4. When a neighbour's in-degree reaches 0, push it into the queue.
5. If processed count equals `numCourses`, the graph is a Directed Acyclic Graph (DAG) and courses can be completed. Otherwise, a cycle exists.
6. Time Complexity: $O(V + E)$ where $V = \text{numCourses}$ and $E = \text{len(prerequisites)}$. Space Complexity: $O(V + E)$ for graph representation.

## TypeScript Implementation

```typescript
export function canFinish(numCourses: number, prerequisites: number[][]): boolean {
  const inDegree: number[] = new Array(numCourses).fill(0);
  const adj: number[][] = Array.from({ length: numCourses }, () => []);

  for (const [course, prereq] of prerequisites) {
    adj[prereq].push(course);
    inDegree[course]++;
  }

  const queue: number[] = [];
  for (let i = 0; i < numCourses; i++) {
    if (inDegree[i] === 0) {
      queue.push(i);
    }
  }

  let processed = 0;
  let head = 0;

  while (head < queue.length) {
    const curr = queue[head++];
    processed++;

    for (const next of adj[curr]) {
      inDegree[next]--;
      if (inDegree[next] === 0) {
        queue.push(next);
      }
    }
  }

  return processed === numCourses;
}
```

## Rust Implementation

```rust
use std::collections::VecDeque;

pub fn can_finish(num_courses: i32, prerequisites: Vec<Vec<i32>>) -> bool {
    let n = num_courses as usize;
    let mut in_degree = vec![0; n];
    let mut adj = vec![Vec::new(); n];

    for edge in prerequisites {
        let course = edge[0] as usize;
        let prereq = edge[1] as usize;
        adj[prereq].push(course);
        in_degree[course] += 1;
    }

    let mut queue = VecDeque::new();
    for (i, &deg) in in_degree.iter().enumerate() {
        if deg == 0 {
            queue.push_back(i);
        }
    }

    let mut processed = 0;
    while let Some(curr) = queue.pop_front() {
        processed += 1;
        for &next in &adj[curr] {
            in_degree[next] -= 1;
            if in_degree[next] == 0 {
                queue.push_back(next);
            }
        }
    }

    processed == n
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_can_finish() {
        assert!(can_finish(2, vec![vec![1, 0]]));
        assert!(!can_finish(2, vec![vec![1, 0], vec![0, 1]]));
    }
}
```
