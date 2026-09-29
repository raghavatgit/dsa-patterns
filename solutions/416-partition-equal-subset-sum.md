# 416. Partition Equal Subset Sum

## Complexity
- Time Complexity: O(n * target) where target = sum / 2
- Space Complexity: O(target) 1D boolean array

## Rust Implementation
```rust
pub fn can_partition(nums: Vec<i32>) -> bool {
    let sum: i32 = nums.iter().sum();
    if sum % 2 != 0 { return false; }
    let target = (sum / 2) as usize;

    let mut dp = vec![false; target + 1];
    dp[0] = true;

    for num in nums {
        let n = num as usize;
        for j in (n..=target).rev() {
            dp[j] = dp[j] || dp[j - n];
        }
    }

    dp[target]
}
```

## TypeScript Implementation
```typescript
export function canPartition(nums: number[]): boolean {
    const sum = nums.reduce((a, b) => a + b, 0);
    if (sum % 2 !== 0) return false;
    const target = sum / 2;

    const dp = new Array(target + 1).fill(false);
    dp[0] = true;

    for (const num of nums) {
        for (let j = target; j >= num; j--) {
            dp[j] = dp[j] || dp[j - num];
        }
    }

    return dp[target];
}
```
