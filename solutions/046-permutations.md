# Problem: Permutations

## Problem Statement
Given an array `nums` of distinct integers, return all the possible permutations. You can return the answer in any order.

## Intuition & Approach
In-Place Swap Backtracking ($O(1)$ Extra Space):
1. Instead of allocating extra visited boolean arrays, maintain permutations in-place by swapping.
2. At position `start`, swap `nums[start]` with `nums[i]` for all $i \ge \text{start}$.
3. Recurse on `start + 1`.
4. Swap back to restore original array order (backtrack).
5. When `start == nums.length`, clone `nums` to results.
6. Time Complexity: $O(N \times N!)$. Space Complexity: $O(N)$ recursion stack depth.

## TypeScript Implementation

```typescript
export function permute(nums: number[]): number[][] {
  const results: number[][] = [];

  function backtrack(start: number) {
    if (start === nums.length) {
      results.push([...nums]);
      return;
    }

    for (let i = start; i < nums.length; i++) {
      const temp = nums[start];
      nums[start] = nums[i];
      nums[i] = temp;

      backtrack(start + 1);

      nums[i] = nums[start];
      nums[start] = temp;
    }
  }

  backtrack(0);
  return results;
}
```

## Rust Implementation

```rust
pub fn permute(mut nums: Vec<i32>) -> Vec<Vec<i32>> {
    let mut results = Vec::new();

    fn backtrack(start: usize, nums: &mut Vec<i32>, results: &mut Vec<Vec<i32>>) {
        if start == nums.len() {
            results.push(nums.clone());
            return;
        }

        for i in start..nums.len() {
            nums.swap(start, i);
            backtrack(start + 1, nums, results);
            nums.swap(start, i);
        }
    }

    backtrack(0, &mut nums, &mut results);
    results
}
```
