# Problem: Permutations II

## Problem Statement
Given a collection of numbers, `nums`, that might contain duplicates, return all possible unique permutations in any order.

## Intuition & Approach
Frequency Map / Used Flags Backtracking:
1. Sort `nums` in ascending order.
2. Maintain a `used` boolean array of size $N$.
3. At each step, consider element `nums[i]`:
   - If `used[i] == true`, skip.
   - If $i > 0$ and `nums[i] == nums[i - 1]` and `!used[i - 1]`, skip! (The previous duplicate was already processed at this position, preventing duplicate branch generation).
4. Time Complexity: $O(N \times N!)$. Space Complexity: $O(N)$ for `used` array and recursion stack.

## TypeScript Implementation

```typescript
export function permuteUnique(nums: number[]): number[][] {
  nums.sort((a, b) => a - b);
  const results: number[][] = [];
  const curr: number[] = [];
  const used: boolean[] = new Array(nums.length).fill(false);

  function backtrack() {
    if (curr.length === nums.length) {
      results.push([...curr]);
      return;
    }

    for (let i = 0; i < nums.length; i++) {
      if (used[i]) continue;
      if (i > 0 && nums[i] === nums[i - 1] && !used[i - 1]) continue;

      used[i] = true;
      curr.push(nums[i]);
      backtrack();
      curr.pop();
      used[i] = false;
    }
  }

  backtrack();
  return results;
}
```
