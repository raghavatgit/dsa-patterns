# Problem: Clone Graph

## Problem Statement
Given a reference of a node in a connected undirected graph, return a deep copy (clone) of the graph. Each node in the graph contains a value (`int`) and a list (`List[Node]`) of its neighbors.

## Intuition & Approach
Depth First Search with Map Pointer Memoization:
1. Maintain a Hash Map mapping `original_node -> cloned_node` to prevent infinite loops on cyclical graphs and duplicate node instantiation.
2. If current node is null, return null.
3. If current node already exists in map, return the cached cloned node immediately.
4. Otherwise, instantiate a new node with `original.val`, record it in map, and recursively clone all neighbours.
5. Time Complexity: $O(V + E)$ visiting every vertex and edge once. Space Complexity: $O(V)$ hash map and recursion stack.

## TypeScript Implementation

```typescript
export class Node {
  val: number;
  neighbors: Node[];
  constructor(val: number = 0, neighbors: Node[] = []) {
    this.val = val;
    this.neighbors = neighbors;
  }
}

export function cloneGraph(node: Node | null): Node | null {
  if (node === null) return null;

  const visited = new Map<Node, Node>();

  function dfs(curr: Node): Node {
    if (visited.has(curr)) {
      return visited.get(curr)!;
    }

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
