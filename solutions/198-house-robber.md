# 198. House Robber

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1) using two variables

## Invariant
`dp[i] = max(dp[i-1], dp[i-2] + nums[i])`

## Rust Implementation
```rust
pub fn rob(nums: Vec<i32>) -> i32 {
    let mut prev2 = 0;
    let mut prev1 = 0;
    for num in nums {
        let curr = prev1.max(prev2 + num);
        prev2 = prev1;
        prev1 = curr;
    }
    prev1
}
```

## TypeScript Implementation
```typescript
export function rob(nums: number[]): number {
    let prev2 = 0;
    let prev1 = 0;
    for (const num of nums) {
        const curr = Math.max(prev1, prev2 + num);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```
