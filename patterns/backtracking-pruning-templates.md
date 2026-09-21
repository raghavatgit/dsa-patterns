# Pattern: Backtracking Pruning and State Space Exploration

## Overview
Backtracking systematically explores the solution space of combinatorial search problems (permutations, combinations, subsets, partitions). It models the search as a tree and prunes invalid branches early via bounding functions.

## Canonical Pruning Techniques
1. **Sibling Deduplication**:
   When inputs contain duplicates, sort first:
   ```cpp
   if (i > start && nums[i] == nums[i - 1]) continue;
   ```
2. **Early Boundary Break**:
   In target sum problems:
   ```cpp
   if (nums[i] > remaining_target) break; // Array must be sorted
   ```
3. **In-Place State Modification**:
   Avoid cloning arrays at each step by pushing, recursing, and popping, or swapping elements directly.
