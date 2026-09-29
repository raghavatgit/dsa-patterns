# 40. Combination Sum II

## Complexity
- Time Complexity: O(2^n)
- Space Complexity: O(n)

## TypeScript Implementation
```typescript
export function combinationSum2(candidates: number[], target: number): number[][] {
    candidates.sort((a, b) => a - b);
    const res: number[][] = [];
    const curr: number[] = [];

    const backtrack = (start: number, rem: number) => {
        if (rem === 0) {
            res.push([...curr]);
            return;
        }
        for (let i = start; i < candidates.length; i++) {
            if (candidates[i] > rem) break;
            if (i > start && candidates[i] === candidates[i - 1]) continue;
            curr.push(candidates[i]);
            backtrack(i + 1, rem - candidates[i]);
            curr.pop();
        }
    };

    backtrack(0, target);
    return res;
}
```
