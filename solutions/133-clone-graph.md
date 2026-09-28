# 133. Clone Graph

## Complexity
- Time Complexity: O(V + E)
- Space Complexity: O(V)

## TypeScript Implementation
```typescript
export class Node {
    val: number;
    neighbors: Node[];
    constructor(val = 0, neighbors = []) {
        this.val = val;
        this.neighbors = neighbors;
    }
}

export function cloneGraph(node: Node | null): Node | null {
    if (!node) return null;
    const visited = new Map<Node, Node>();

    const dfs = (curr: Node): Node => {
        if (visited.has(curr)) return visited.get(curr)!;
        const clone = new Node(curr.val);
        visited.set(curr, clone);

        for (const neighbor of curr.neighbors) {
            clone.neighbors.push(dfs(neighbor));
        }
        return clone;
    };

    return dfs(node);
}
```
