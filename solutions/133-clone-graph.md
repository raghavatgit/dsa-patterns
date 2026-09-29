# 133. Clone Graph

## Complexity
- Time Complexity: O(V + E)
- Space Complexity: O(V) hash map

## TypeScript Implementation
```typescript
class Node {
    val: number;
    neighbors: Node[];
    constructor(val?: number, neighbors?: Node[]) {
        this.val = (val === undefined ? 0 : val);
        this.neighbors = (neighbors === undefined ? [] : neighbors);
    }
}

export function cloneGraph(node: Node | null): Node | null {
    if (!node) return null;
    const visited = new Map<Node, Node>();

    function dfs(curr: Node): Node {
        if (visited.has(curr)) return visited.get(curr)!;
        const copy = new Node(curr.val);
        visited.set(curr, copy);
        for (const neighbor of curr.neighbors) {
            copy.neighbors.push(dfs(neighbor));
        }
        return copy;
    }

    return dfs(node);
}
```
