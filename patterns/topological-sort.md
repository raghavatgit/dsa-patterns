# Topological Sort (Kahn's Algorithm & DFS)

## Concept
A topological sort of a directed graph is a linear ordering of its vertices such that for every directed edge `(u, v)`, vertex `u` comes before vertex `v` in the ordering. Topological sort exists if and only if the graph is a Directed Acyclic Graph (DAG).

Kahn's Algorithm employs an in-degree counting approach:
1. Compute in-degree (number of incoming edges) for every node.
2. Enqueue all nodes with in-degree equal to 0.
3. While the queue is not empty, dequeue node `u`, append `u` to the result, and decrement the in-degree of all neighbors.
4. If a neighbor's in-degree drops to 0, enqueue it.
5. If result length != total nodes, a cycle exists.

## TypeScript Implementation

```typescript
export function topologicalSort(numNodes: number, edges: [number, number][]): number[] {
  const inDegree: number[] = new Array(numNodes).fill(0);
  const adjList: Map<number, number[]> = new Map();

  for (let i = 0; i < numNodes; i++) {
    adjList.set(i, []);
  }

  for (const [u, v] of edges) {
    adjList.get(u)!.push(v);
    inDegree[v]++;
  }

  const queue: number[] = [];
  for (let i = 0; i < numNodes; i++) {
    if (inDegree[i] === 0) {
      queue.push(i);
    }
  }

  const sortedOrder: number[] = [];
  while (queue.length > 0) {
    const curr = queue.shift()!;
    sortedOrder.push(curr);

    for (const neighbor of adjList.get(curr)!) {
      inDegree[neighbor]--;
      if (inDegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  if (sortedOrder.length !== numNodes) {
    throw new Error("Graph contains a cycle; topological sort impossible");
  }

  return sortedOrder;
}
```

## Complexity Analysis
* **Time Complexity:** O(V + E) where V is vertices and E is edges.
* **Space Complexity:** O(V + E) for adjacency list and in-degree tracking array.
