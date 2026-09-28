# 785. Is Graph Bipartite?

## Complexity
- Time Complexity: O(V + E)
- Space Complexity: O(V)

## TypeScript Implementation
```typescript
export function isBipartite(graph: number[][]): boolean {
    const n = graph.length;
    const colors = new Array(n).fill(0); // 0: unvisited, 1: red, -1: blue

    for (let i = 0; i < n; i++) {
        if (colors[i] !== 0) continue;
        const queue: number[] = [i];
        colors[i] = 1;

        while (queue.length > 0) {
            const u = queue.shift()!;
            for (const v of graph[u]) {
                if (colors[v] === 0) {
                    colors[v] = -colors[u];
                    queue.push(v);
                } else if (colors[v] === colors[u]) {
                    return false;
                }
            }
        }
    }

    return true;
}
```
