# Connected Components in Undirected Graphs (DFS & BFS)

## Concept
A connected component in an undirected graph is a maximal subgraph in which any two vertices are connected to each other by paths. 

Finding all connected components labels each vertex with an integer `component_id`:
1. Maintain a boolean `visited[V]` array and an integer `component[V]` array.
2. Iterate through all vertices `u = 0` to `V - 1`.
3. If vertex `u` has not been visited, increment `component_id` and initiate a Depth-First Search (DFS) or Breadth-First Search (BFS) to traverse and mark the entire reachable component.

## C Implementation (Adjacency List)

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

typedef struct Node {
    int dest;
    struct Node* next;
} Node;

typedef struct Graph {
    int V;
    Node** adjLists;
} Graph;

Node* createNode(int d) {
    Node* n = (Node*)malloc(sizeof(Node));
    n->dest = d;
    n->next = NULL;
    return n;
}

Graph* createGraph(int V) {
    Graph* g = (Graph*)malloc(sizeof(Graph));
    g->V = V;
    g->adjLists = (Node**)calloc(V, sizeof(Node*));
    return g;
}

void addEdge(Graph* g, int src, int dest) {
    Node* n1 = createNode(dest);
    n1->next = g->adjLists[src];
    g->adjLists[src] = n1;

    Node* n2 = createNode(src);
    n2->next = g->adjLists[dest];
    g->adjLists[dest] = n2;
}

void dfsComponent(Graph* g, int u, int compId, bool visited[], int component[]) {
    visited[u] = true;
    component[u] = compId;

    Node* temp = g->adjLists[u];
    while (temp != NULL) {
        int v = temp->dest;
        if (!visited[v]) {
            dfsComponent(g, v, compId, visited, component);
        }
        temp = temp->next;
    }
}
```

## TypeScript Implementation

```typescript
export function findConnectedComponents(
  numVertices: number,
  edges: [number, number][]
): { componentCount: number; components: number[] } {
  const adjList: Map<number, number[]> = new Map();
  for (let i = 0; i < numVertices; i++) {
    adjList.set(i, []);
  }

  for (const [u, v] of edges) {
    adjList.get(u)!.push(v);
    adjList.get(v)!.push(u);
  }

  const visited: boolean[] = new Array(numVertices).fill(false);
  const component: number[] = new Array(numVertices).fill(0);
  let componentCount = 0;

  function dfs(u: number, compId: number) {
    visited[u] = true;
    component[u] = compId;

    for (const v of adjList.get(u)!) {
      if (!visited[v]) {
        dfs(v, compId);
      }
    }
  }

  for (let i = 0; i < numVertices; i++) {
    if (!visited[i]) {
      componentCount++;
      dfs(i, componentCount);
    }
  }

  return { componentCount, components: component };
}
```

## Rust Implementation

```rust
pub fn find_connected_components(
    num_vertices: usize,
    edges: &[(usize, usize)],
) -> (usize, Vec<usize>) {
    let mut adj: Vec<Vec<usize>> = vec![Vec::new(); num_vertices];
    for &(u, v) in edges {
        adj[u].push(v);
        adj[v].push(u);
    }

    let mut visited = vec![false; num_vertices];
    let mut component = vec![0; num_vertices];
    let mut component_count = 0;

    for i in 0..num_vertices {
        if !visited[i] {
            component_count += 1;
            let mut stack = vec![i];
            visited[i] = true;
            component[i] = component_count;

            while let Some(u) = stack.pop() {
                for &v in &adj[u] {
                    if !visited[v] {
                        visited[v] = true;
                        component[v] = component_count;
                        stack.push(v);
                    }
                }
            }
        }
    }

    (component_count, component)
}
```

## Complexity Analysis
* **Time Complexity:** O(V + E) since every vertex and edge is traversed exactly once.
* **Space Complexity:** O(V + E) for the adjacency list and O(V) for the visited and component mapping tables.
