# 90. Subsets II

## Complexity
- Time Complexity: O(n * 2^n)
- Space Complexity: O(n * 2^n)

## TypeScript Implementation
```typescript
export function subsetsWithDup(nums: number[]): number[][] {
    nums.sort((a, b) => a - b);
    const res: number[][] = [];
    const curr: number[] = [];

    const backtrack = (start: number) => {
        res.push([...curr]);
        for (let i = start; i < nums.length; i++) {
            if (i > start && nums[i] === nums[i - 1]) continue;
            curr.push(nums[i]);
            backtrack(i + 1);
            curr.pop();
        }
    };

    backtrack(0);
    return res;
}
```
