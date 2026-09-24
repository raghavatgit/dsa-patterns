# Pattern: Sliding Window and Two-Pointer Mechanics

## Categories
1. **Fixed Window**: Window length $K$ is invariant. Advance both pointers synchronously. Maintain running sum/state.
2. **Dynamic Window (Expand / Contract)**:
   - Expand `right` until validity condition is met or broken.
   - Contract `left` while condition holds (minimization) or fails (restoration).
3. **Inward Shrinking Two-Pointer**:
   - Pointers start at $0$ and $N - 1$.
   - Greedily advance the bottleneck pointer (e.g., Container With Most Water, 2Sum Sorted, 3Sum).

## Template: Dynamic Sliding Window
```cpp
int left = 0;
for (int right = 0; right < n; ++right) {
    // 1. Add nums[right] to window state
    while (window_condition_broken()) {
        // 2. Remove nums[left] from window state
        left++;
    }
    // 3. Update answer with valid window [left, right]
}
```
