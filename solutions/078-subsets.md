# Problem: Subsets

## Problem Statement
Given an integer array `nums` of unique elements, return all possible subsets (the power set). The solution set must not contain duplicate subsets. Return the solution in any order.

## Intuition & Approach
Backtracking / Cascading:
1. Every element has two choices: include in the current subset or omit.
2. Maintain a running path array `curr`.
3. Add a clone of `curr` to the result set at every node of the recursion tree.
4. Iterate index $i$ from `start` to $N - 1$:
   - Push `nums[i]` to `curr`.
   - Recurse on `i + 1`.
   - Pop `nums[i]` from `curr` (backtrack).
5. Total subsets generated is $2^N$.
6. Time Complexity: $O(N \times 2^N)$. Space Complexity: $O(N)$ recursion depth.

## TypeScript Implementation

```typescript
export function subsets(nums: number[]): number[][] {
  const results: number[][] = [];
  const curr: number[] = [];

  function backtrack(start: number) {
    results.push([...curr]);

    for (let i = start; i < nums.length; i++) {
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
pub fn subsets(nums: Vec<i32>) -> Vec<Vec<i32>> {
    let mut results = Vec::with_capacity(1 << nums.len());
    let mut curr = Vec::with_capacity(nums.len());

    fn backtrack(start: usize, nums: &[i32], curr: &mut Vec<i32>, results: &mut Vec<Vec<i32>>) {
        results.push(curr.clone());

        for i in start..nums.len() {
            curr.push(nums[i]);
            backtrack(i + 1, nums, curr, results);
            curr.pop();
        }
    }

    backtrack(0, &nums, &mut curr, &mut results);
    results
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_subsets() {
        let res = subsets(vec![1, 2, 3]);
        assert_eq!(res.len(), 8);
    }
}
```
