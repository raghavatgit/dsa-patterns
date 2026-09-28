# 210. Course Schedule II

## Complexity
- Time Complexity: O(V + E)
- Space Complexity: O(V + E)

## TypeScript Implementation
```typescript
export function findOrder(numCourses: number, prerequisites: number[][]): number[] {
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
