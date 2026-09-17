# Problem: House Robber

## Problem Statement
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, but adjacent houses have security systems connected that automatically contact the police if two adjacent houses are broken into on the same night. Return the maximum amount of money you can rob tonight without alerting the police.

## Intuition & Approach
Dynamic Programming recurrence:
`dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])`
Notice that calculating `dp[i]` only depends on the previous two states (`prev1` and `prev2`). We can reduce space complexity from $O(N)$ to $O(1)$ by maintaining two scalar variables.

## TypeScript Implementation

```typescript
export function rob(nums: number[]): number {
  if (nums.length === 0) return 0;
  if (nums.length === 1) return nums[0];

  let prev2 = 0;
  let prev1 = 0;

  for (const num of nums) {
    const current = Math.max(prev1, prev2 + num);
    prev2 = prev1;
    prev1 = current;
  }

  return prev1;
}
```

## Rust Implementation

```rust
pub fn rob(nums: &[i32]) -> i32 {
    let mut prev2 = 0;
    let mut prev1 = 0;

    for &num in nums {
        let current = prev1.max(prev2 + num);
        prev2 = prev1;
        prev1 = current;
    }

    prev1
}
```

## Complexity Analysis
* **Time Complexity:** O(N) single-pass iteration.
* **Space Complexity:** O(1) space optimization using two scalar variables.
