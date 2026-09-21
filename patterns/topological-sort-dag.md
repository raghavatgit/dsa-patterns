# Pattern: Topological Sorting and Directed Acyclic Graph (DAG) Traversal

## Overview
A topological sort of a directed graph is a linear ordering of its vertices such that for every directed edge $(u, v)$, vertex $u$ comes before $v$ in the ordering.
A topological sort is possible if and only if the graph has no directed cycles (it is a DAG).

## The Two Canonical Formulations
1. **Kahn's Algorithm (BFS In-Degree Queue)**:
   - Compute in-degree for all $V$ vertices.
   - Enqueue vertices with in-degree 0.
   - Dequeue $u$, append to order, decrement in-degree of all neighbors $v$.
   - If in-degree of $v$ drops to 0, enqueue $v$.
   - If output length $< V$, graph contains a cycle.
2. **Tarjan's Algorithm (DFS Post-Order LIFO Stack)**:
   - 3-state coloring: 0 (white/unvisited), 1 (gray/visiting), 2 (black/visited).
   - Recurse on neighbors. If neighbor is in state 1, back-edge detected (cycle).
   - Push vertex to stack upon post-order completion.
   - Reverse stack for valid topological order.
