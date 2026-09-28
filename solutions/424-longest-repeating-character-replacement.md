# 424. Longest Repeating Character Replacement

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1) frequency array of size 26

## TypeScript Implementation
```typescript
export function characterReplacement(s: string, k: number): number {
    const counts = new Array(26).fill(0);
    let left = 0, maxCount = 0, maxLen = 0;

    for (let right = 0; right < s.length; right++) {
        const idx = s.charCodeAt(right) - 65;
        counts[idx]++;
        maxCount = Math.max(maxCount, counts[idx]);

        while ((right - left + 1) - maxCount > k) {
            counts[s.charCodeAt(left) - 65]--;
            left++;
        }

        maxLen = Math.max(maxLen, right - left + 1);
    }

    return maxLen;
}
```
