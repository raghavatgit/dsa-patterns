# Problem: Combination Sum II

## Problem Statement
Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`. Each number in `candidates` may only be used once in the combination.

## Intuition & Approach
Bounded Backtracking with Duplicate Pruning:
1. Sort `candidates` ascending.
2. Backtrack with `i + 1` so each index is used at most once.
3. At the same tree depth, skip duplicate values: if `i > start && candidates[i] == candidates[i - 1]`, `continue`.
4. Early loop break when `candidates[i] > remain`.
5. Time Complexity: $O(2^N)$. Space Complexity: $O(N)$ recursion depth.

## TypeScript Implementation

```typescript
export function combinationSum2(candidates: number[], target: number): number[][] {
  candidates.sort((a, b) => a - b);
  const results: number[][] = [];
  const curr: number[] = [];

  function backtrack(start: number, remain: number) {
    if (remain === 0) {
      results.push([...curr]);
      return;
    }

    for (let i = start; i < candidates.length; i++) {
      if (i > start && candidates[i] === candidates[i - 1]) continue;
      const c = candidates[i];
      if (c > remain) break;

      curr.push(c);
      backtrack(i + 1, remain - c);
      curr.pop();
    }
  }

  backtrack(0, target);
  return results;
}
```
