# 416. Partition Equal Subset Sum

## Problem Statement
Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or `false` otherwise.

---

## TypeScript Implementation

```typescript
export function canPartition(nums: number[]): boolean {
  const sum = nums.reduce((acc, curr) => acc + curr, 0);
  if (sum % 2 !== 0) return false;

  const target = sum / 2;
  const dp = new Array<boolean>(target + 1).fill(false);
  dp[0] = true;

  for (const num of nums) {
    for (let j = target; j >= num; j--) {
      dp[j] = dp[j] || dp[j - num];
    }
    if (dp[target]) return true;
  }

  return dp[target];
}
```

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn can_partition(nums: Vec<i32>) -> bool {
        let sum: i32 = nums.iter().sum();
        if sum % 2 != 0 {
            return false;
        }

        let target = (sum / 2) as usize;
        let mut dp = vec![false; target + 1];
        dp[0] = true;

        for num in nums {
            let n = num as usize;
            for j in (n..=target).rev() {
                dp[j] = dp[j] || dp[j - n];
            }
            if dp[target] {
                return true;
            }
        }

        dp[target]
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(n * target)` where `target = sum / 2`.
- Space Complexity: `O(target)` using a 1D boolean array traversed in reverse.
