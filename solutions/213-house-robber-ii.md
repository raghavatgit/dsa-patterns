# 213. House Robber II

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## TypeScript Implementation
```typescript
export function rob(nums: number[]): number {
    if (nums.length === 1) return nums[0];

    const robLinear = (arr: number[]): number => {
        let rob1 = 0, rob2 = 0;
        for (const n of arr) {
            const temp = Math.max(n + rob1, rob2);
            rob1 = rob2;
            rob2 = temp;
        }
        return rob2;
    };

    return Math.max(robLinear(nums.slice(0, -1)), robLinear(nums.slice(1)));
}
```
