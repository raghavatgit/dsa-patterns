# 323. Number of Connected Components in an Undirected Graph

## Complexity
- Time Complexity: O(E * alpha(V))
- Space Complexity: O(V)

## TypeScript Implementation
```typescript
export function countComponents(n: number, edges: number[][]): number {
    const parent = Array.from({ length: n }, (_, i) => i);
    let count = n;

    const find = (i: number): number => {
        let curr = i;
        while (curr !== parent[curr]) {
            parent[curr] = parent[parent[curr]];
            curr = parent[curr];
        }
        return curr;
    };

    for (const [u, v] of edges) {
        const rootU = find(u);
        const rootV = find(v);
        if (rootU !== rootV) {
            parent[rootU] = rootV;
            count--;
        }
    }

    return count;
}
```
