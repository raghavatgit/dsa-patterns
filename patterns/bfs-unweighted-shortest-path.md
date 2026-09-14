# BFS Unweighted Shortest Path and Hop Count

## Concept
In an unweighted graph (or graph where every edge has equal weight), Breadth-First Search (BFS) is guaranteed to discover the shortest path from a source vertex `s` to any reachable vertex `v`.

* **Distance Invariant:** A vertex at hop distance `k` is processed strictly before any vertex at distance `k + 1`.
* **Hop Count Array:** Initializing `dist[v] = -1` for all vertices and `dist[src] = 0` tracks both visitation status and shortest hop count simultaneously without requiring a separate boolean `visited[]` array.

## C Implementation (Adjacency List & Queue)

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int dest;
    struct Node* next;
} Node;

typedef struct Graph {
    int V;
    Node** adjLists;
} Graph;

void bfsShortestHop(Graph* g, int source) {
    int* dist = (int*)malloc(g->V * sizeof(int));
    for (int i = 0; i < g->V; i++) dist[i] = -1;

    int* queue = (int*)malloc(g->V * sizeof(int));
    int front = 0, rear = 0;

    dist[source] = 0;
    queue[rear++] = source;

    printf("=== BFS Traversal Sequence ===\nOrder: ");

    while (front < rear) {
        int u = queue[front++];
        printf("%d ", u);

        Node* temp = g->adjLists[u];
        while (temp != NULL) {
            int v = temp->dest;
            if (dist[v] == -1) {
                dist[v] = dist[u] + 1; // Shortest hop count
                queue[rear++] = v;
            }
            temp = temp->next;
        }
    }
    printf("\n\n----------------------------------------\n");
    printf(" Vertex | Visited | Shortest Hop Count\n");
    printf("----------------------------------------\n");
    for (int i = 0; i < g->V; i++) {
        if (dist[i] != -1) {
            printf("   %2d   | YES     | %d hops\n", i, dist[i]);
        } else {
            printf("   %2d   | NO      | Unreachable\n", i);
        }
    }
    printf("----------------------------------------\n");

    free(dist);
    free(queue);
}
```

## TypeScript Implementation

```typescript
export interface BFSHopResult {
  traversalOrder: number[];
  hopCounts: number[];
}

export function bfsShortestHop(
  numVertices: number,
  adjList: Map<number, number[]>,
  source: number
): BFSHopResult {
  const dist: number[] = new Array(numVertices).fill(-1);
  const traversalOrder: number[] = [];
  const queue: number[] = [];

  dist[source] = 0;
  queue.push(source);

  while (queue.length > 0) {
    const u = queue.shift()!;
    traversalOrder.push(u);

    for (const v of adjList.get(u) || []) {
      if (dist[v] === -1) {
        dist[v] = dist[u] + 1;
        queue.push(v);
      }
    }
  }

  return { traversalOrder, hopCounts: dist };
}
```

## Rust Implementation

```rust
use std::collections::VecDeque;

pub struct BFSHopResult {
    pub order: Vec<usize>,
    pub hop_counts: Vec<Option<usize>>,
}

pub fn bfs_shortest_hop(
    num_vertices: usize,
    adj: &[Vec<usize>],
    source: usize,
) -> BFSHopResult {
    let mut dist: Vec<Option<usize>> = vec![None; num_vertices];
    let mut order = Vec::with_capacity(num_vertices);
    let mut queue = VecDeque::new();

    dist[source] = Some(0);
    queue.push_back(source);

    while let Some(u) = queue.pop_front() {
        order.push(u);
        let current_hops = dist[u].unwrap();

        for &v in &adj[u] {
            if dist[v].is_none() {
                dist[v] = Some(current_hops + 1);
                queue.push_back(v);
            }
        }
    }

    BFSHopResult { order, hop_counts: dist }
}
```

## Complexity Analysis
* **Time Complexity:** O(V + E) linear in vertices and edges.
* **Space Complexity:** O(V) for the FIFO queue and distance table.
