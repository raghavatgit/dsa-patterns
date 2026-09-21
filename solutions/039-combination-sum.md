# Problem: Combination Sum

## Problem Statement
Given an array of distinct integers `candidates` and a target integer `target`, return a list of all unique combinations of `candidates` where the chosen numbers sum to `target`. You may return the combinations in any order. The same number may be chosen from `candidates` an unlimited number of times.

## Intuition & Approach
Unbounded Backtracking with Candidate Pruning:
1. Sort `candidates` ascending to allow early exit when candidate exceeds remaining target.
2. Maintain `remain = target - sum(curr)`.
3. If `remain == 0`, valid combination found: clone `curr` into results.
4. If candidate $c > \text{remain}$, break loop immediately (because all subsequent candidates are even larger).
5. Recurse with start index `i` (not `i + 1`), allowing candidate to be reused.
6. Time Complexity: $O(N^{\text{target} / \min(c)})$. Space Complexity: $O(\text{target} / \min(c))$ recursion depth.

## TypeScript Implementation

```typescript
export function combinationSum(candidates: number[], target: number): number[][] {
  candidates.sort((a, b) => a - b);
  const results: number[][] = [];
  const curr: number[] = [];

  function backtrack(start: number, remain: number) {
    if (remain === 0) {
      results.push([...curr]);
      return;
    }

    for (let i = start; i < candidates.length; i++) {
      const c = candidates[i];
      if (c > remain) break;

      curr.push(c);
      backtrack(i, remain - c);
      curr.pop();
    }
  }

  backtrack(0, target);
  return results;
}
```

## Rust Implementation

```rust
pub fn combination_sum(mut candidates: Vec<i32>, target: i32) -> Vec<Vec<i32>> {
    candidates.sort_unstable();
    let mut results = Vec::new();
    let mut curr = Vec::new();

    fn backtrack(start: usize, remain: i32, candidates: &[i32], curr: &mut Vec<i32>, results: &mut Vec<Vec<i32>>) {
        if remain == 0 {
            results.push(curr.clone());
            return;
        }

        for i in start..candidates.len() {
            let c = candidates[i];
            if c > remain { break; }

            curr.push(c);
            backtrack(i, remain - c, candidates, curr, results);
            curr.pop();
        }
    }

    backtrack(0, target, &candidates, &mut curr, &mut results);
    results
}
```
