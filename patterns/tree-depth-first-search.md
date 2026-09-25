# Pattern: Tree Depth-First Search (DFS)

## Recurrence Archetypes
1. **Divide and Conquer (Bottom-Up)**:
   - Calculate left subtree state and right subtree state independently.
   - Aggregate result at current node (e.g., Maximum Depth, Diameter, LCA).
2. **Top-Down Accumulator**:
   - Pass running context downward into child calls (e.g., Path Sum, Valid BST range bounds).
3. **Inorder BST Traversal**:
   - Monotonic property: in-order visit on BST guarantees non-decreasing order of elements.
