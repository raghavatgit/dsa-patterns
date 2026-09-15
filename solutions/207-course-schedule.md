# Problem: Course Schedule (Cycle Detection in DAG)

## Problem Statement
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [a_i, b_i]` indicates that you must take course `b_i` first if you want to take course `a_i`. Return `true` if you can finish all courses, otherwise `false`.

## Intuition & Approach
The prerequisites define directed edges `b_i -> a_i`. Taking all courses is possible if and only if the dependency graph contains no directed cycles.
Kahn's Algorithm (BFS topological sort):
1. Calculate in-degree for all vertices.
2. Push all vertices with in-degree = 0 to a FIFO queue.
3. Dequeue course, decrement neighbors' in-degrees. If neighbor in-degree hits 0, enqueue it.
4. If total processed courses == `numCourses`, return `true`.

## TypeScript Implementation

```typescript
export function canFinish(numCourses: number, prerequisites: [number, number][]): boolean {
  const inDegree: number[] = new Array(numCourses).fill(0);
  const adj = new Map<number, number[]>();

  for (let i = 0; i < numCourses; i++) {
    adj.set(i, []);
  }

  for (const [course, prereq] of prerequisites) {
    adj.get(prereq)!.push(course);
    inDegree[course]++;
  }

  const queue: number[] = [];
  for (let i = 0; i < numCourses; i++) {
    if (inDegree[i] === 0) {
      queue.push(i);
    }
  }

  let takenCount = 0;
  while (queue.length > 0) {
    const curr = queue.shift()!;
    takenCount++;

    for (const neighbor of adj.get(curr)!) {
      inDegree[neighbor]--;
      if (inDegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  return takenCount === numCourses;
}
```

## Rust Implementation

```rust
use std::collections::VecDeque;

pub fn can_finish(num_courses: i32, prerequisites: &[[i32; 2]]) -> bool {
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

    let mut completed = 0;
    while let Some(u) = queue.pop_front() {
        completed += 1;
        for &v in &adj[u] {
            in_degree[v] -= 1;
            if in_degree[v] == 0 {
                queue.push_back(v);
            }
        }
    }

    completed == n
}
```

## Complexity Analysis
* **Time Complexity:** O(V + E) where V is courses and E is prerequisite pairs.
* **Space Complexity:** O(V + E) for adjacency list representation and in-degree table.
