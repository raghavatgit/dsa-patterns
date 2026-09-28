# 416. Partition Equal Subset Sum

## Complexity
- Time Complexity: O(n * sum)
- Space Complexity: O(sum)

## TypeScript Implementation
```typescript
export function canPartition(nums: number[]): boolean {
    const total = nums.reduce((acc, cur) => acc + cur, 0);
    if (total % 2 !== 0) return false;
    const target = total / 2;

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
