# Problem: Course Schedule II (Topological Sort)

## Problem Statement
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.
Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses (cycle exists), return an empty array.

## Intuition & Approach
DFS with 3-State Cycle Detection (Cormen DAA Standard):
1. Color states for each vertex:
   - State 0 (`UNVISITED`): Node has not been touched.
   - State 1 (`VISITING`): Node is currently on the active DFS recursion stack. If we encounter a neighbor in state 1, a back-edge exists (directed cycle detected).
   - State 2 (`VISITED`): Node and all its descendants have been completely processed.
2. For each unvisited vertex, execute DFS.
3. Upon finishing a vertex, push it onto a LIFO stack or append to results.
4. Reverse or pop from stack to obtain valid topological ordering.
5. Time Complexity: $O(V + E)$. Space Complexity: $O(V + E)$ adjacency list and recursion stack.

## C Implementation (DAA Standard Adjacency List)

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define MAX_V 1000

typedef struct Node {
    int dest;
    struct Node* next;
} Node;

Node* adj[MAX_V];
int visited[MAX_V]; // 0: UNVISITED, 1: VISITING, 2: VISITED
int topoStack[MAX_V];
int topoTop = -1;
bool hasCycle = false;

void addEdge(int u, int v) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->dest = v;
    newNode->next = adj[u];
    adj[u] = newNode;
}

void dfs(int u) {
    visited[u] = 1; // Mark VISITING

    Node* curr = adj[u];
    while (curr != NULL) {
        int v = curr->dest;
        if (visited[v] == 1) {
            hasCycle = true; // Back-edge found
            return;
        }
        if (visited[v] == 0) {
            dfs(v);
            if (hasCycle) return;
        }
        curr = curr->next;
    }

    visited[u] = 2; // Mark VISITED
    topoStack[++topoTop] = u;
}

int* findOrder(int numCourses, int prerequisitesSize, int** prerequisites, int* returnSize) {
    for (int i = 0; i < numCourses; i++) {
        adj[i] = NULL;
        visited[i] = 0;
    }
    topoTop = -1;
    hasCycle = false;

    for (int i = 0; i < prerequisitesSize; i++) {
        addEdge(prerequisites[i][1], prerequisites[i][0]);
    }

    for (int i = 0; i < numCourses; i++) {
        if (visited[i] == 0) {
            dfs(i);
            if (hasCycle) {
                *returnSize = 0;
                return NULL;
            }
        }
    }

    int* order = (int*)malloc(numCourses * sizeof(int));
    *returnSize = numCourses;
    for (int i = 0; i < numCourses; i++) {
        order[i] = topoStack[topoTop--];
    }
    return order;
}
```

## Rust Implementation

```rust
pub fn find_order(num_courses: i32, prerequisites: Vec<Vec<i32>>) -> Vec<i32> {
    let n = num_courses as usize;
    let mut adj = vec![Vec::new(); n];
    for edge in prerequisites {
        adj[edge[1] as usize].push(edge[0] as usize);
    }

    let mut state = vec![0; n]; // 0: unvisited, 1: visiting, 2: visited
    let mut order = Vec::with_capacity(n);
    let mut has_cycle = false;

    fn dfs(u: usize, adj: &Vec<Vec<usize>>, state: &mut Vec<i32>, order: &mut Vec<i32>, has_cycle: &mut bool) {
        if *has_cycle { return; }
        state[u] = 1;

        for &v in &adj[u] {
            if state[v] == 1 {
                *has_cycle = true;
                return;
            }
            if state[v] == 0 {
                dfs(v, adj, state, order, has_cycle);
            }
        }

        state[u] = 2;
        order.push(u as i32);
    }

    for i in 0..n {
        if state[i] == 0 {
            dfs(i, &adj, &mut state, &mut order, &mut has_cycle);
            if has_cycle {
                return vec![];
            }
        }
    }

    order.reverse();
    order
}
```
