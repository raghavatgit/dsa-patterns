# Problem: Subsets II

## Problem Statement
Given an integer array `nums` that may contain duplicates, return all possible subsets (the power set). The solution set must not contain duplicate subsets. Return the solution in any order.

## Intuition & Approach
Sort and Sibling Deduplication:
1. Sort `nums` in ascending order so identical elements are contiguous.
2. In the backtracking loop over index $i$ from `start` to $N - 1$:
   - If $i > \text{start}$ and `nums[i] == nums[i - 1]`, skip iteration (`continue`).
   - This ensures identical values are only picked at the first sibling branch, preventing identical subtrees.
3. Time Complexity: $O(N \log N + N \times 2^N)$. Space Complexity: $O(N)$ recursion depth.

## TypeScript Implementation

```typescript
export function subsetsWithDup(nums: number[]): number[][] {
  nums.sort((a, b) => a - b);
  const results: number[][] = [];
  const curr: number[] = [];

  function backtrack(start: number) {
    results.push([...curr]);

    for (let i = start; i < nums.length; i++) {
      if (i > start && nums[i] === nums[i - 1]) {
        continue;
      }
      curr.push(nums[i]);
      backtrack(i + 1);
      curr.pop();
    }
  }

  backtrack(0);
  return results;
}
```

## Rust Implementation

```rust
pub fn subsets_with_dup(mut nums: Vec<i32>) -> Vec<Vec<i32>> {
    nums.sort_unstable();
    let mut results = Vec::new();
    let mut curr = Vec::new();

    fn backtrack(start: usize, nums: &[i32], curr: &mut Vec<i32>, results: &mut Vec<Vec<i32>>) {
        results.push(curr.clone());

        for i in start..nums.len() {
            if i > start && nums[i] == nums[i - 1] {
                continue;
            }
            curr.push(nums[i]);
            backtrack(i + 1, nums, curr, results);
            curr.pop();
        }
    }

    backtrack(0, &nums, &mut curr, &mut results);
    results
}
```
