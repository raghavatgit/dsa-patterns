# 47. Permutations II

## Complexity
- Time Complexity: O(n * n!)
- Space Complexity: O(n)

## TypeScript Implementation
```typescript
export function permuteUnique(nums: number[]): number[][] {
    nums.sort((a, b) => a - b);
    const res: number[][] = [];
    const curr: number[] = [];
    const visited = new Array(nums.length).fill(false);

    const backtrack = () => {
        if (curr.length === nums.length) {
            res.push([...curr]);
            return;
        }
        for (let i = 0; i < nums.length; i++) {
            if (visited[i]) continue;
            if (i > 0 && nums[i] === nums[i - 1] && !visited[i - 1]) continue;
            visited[i] = true;
            curr.push(nums[i]);
            backtrack();
            curr.pop();
            visited[i] = false;
        }
    };

    backtrack();
    return res;
}
```
