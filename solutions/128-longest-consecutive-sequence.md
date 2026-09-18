# Problem: Longest Consecutive Sequence

## Problem Statement
Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence. You must write an algorithm that runs in $O(N)$ time.

## Intuition & Approach
Hash Set Root Exploration:
1. Insert all numbers into a Hash Set for $O(1)$ existence queries.
2. For each number `x`, check if `x - 1` exists in the set:
   - If `x - 1` exists, `x` is part of an ongoing streak and not the beginning. Skip it.
   - If `x - 1` does not exist, `x` is the root of a potential streak.
3. For sequence roots, count consecutive increments `x + 1, x + 2, ...` until a missing value occurs.
4. Each number is visited at most twice (once in outer loop, at most once during streak expansion).
5. Time Complexity: Strict $O(N)$. Space Complexity: $O(N)$ hash set memory.

## TypeScript Implementation

```typescript
export function longestConsecutive(nums: number[]): number {
  const set = new Set<number>(nums);
  let longestStreak = 0;

  for (const num of set) {
    if (!set.has(num - 1)) {
      let currentNum = num;
      let currentStreak = 1;

      while (set.has(currentNum + 1)) {
        currentNum += 1;
        currentStreak += 1;
      }

      longestStreak = Math.max(longestStreak, currentStreak);
    }
  }

  return longestStreak;
}
```

## Rust Implementation

```rust
use std::collections::HashSet;

pub fn longest_consecutive(nums: Vec<i32>) -> i32 {
    let set: HashSet<i32> = nums.into_iter().collect();
    let mut longest = 0;

    for &num in &set {
        if !set.contains(&(num - 1)) {
            let mut current = num;
            let mut streak = 1;

            while set.contains(&(current + 1)) {
                current += 1;
                streak += 1;
            }

            longest = longest.max(streak);
        }
    }

    longest
}
```
