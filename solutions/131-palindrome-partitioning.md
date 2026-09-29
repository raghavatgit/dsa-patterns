# 131. Palindrome Partitioning

## Complexity
- Time Complexity: O(n * 2^n)
- Space Complexity: O(n)

## TypeScript Implementation
```typescript
export function partition(s: string): string[][] {
    const res: string[][] = [];
    const curr: string[] = [];

    const isPalindrome = (l: number, r: number) => {
        while (l < r) {
            if (s[l++] !== s[r--]) return false;
        }
        return true;
    };

    const backtrack = (start: number) => {
        if (start === s.length) {
            res.push([...curr]);
            return;
        }
        for (let end = start; end < s.length; end++) {
            if (isPalindrome(start, end)) {
                curr.push(s.substring(start, end + 1));
                backtrack(end + 1);
                curr.pop();
            }
        }
    };

    backtrack(0);
    return res;
}
```
