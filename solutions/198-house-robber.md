# 198. House Robber

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## TypeScript Implementation
```typescript
export function rob(nums: number[]): number {
    let rob1 = 0, rob2 = 0;
    for (const n of nums) {
        const temp = Math.max(n + rob1, rob2);
        rob1 = rob2;
        rob2 = temp;
    }
    return rob2;
}
```
