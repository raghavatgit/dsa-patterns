# 76. Minimum Window Substring

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(k)

## TypeScript Implementation
```typescript
export function minWindow(s: string, t: string): string {
    if (!s || !t || s.length < t.length) return "";
    const targetMap = new Map<string, number>();
    for (const c of t) targetMap.set(c, (targetMap.get(c) || 0) + 1);

    const windowMap = new Map<string, number>();
    let left = 0, right = 0, required = targetMap.size, formed = 0;
    let minLen = Infinity, minStart = 0;

    while (right < s.length) {
        const c = s[right];
        windowMap.set(c, (windowMap.get(c) || 0) + 1);
        if (targetMap.has(c) && windowMap.get(c) === targetMap.get(c)) formed++;

        while (left <= right && formed === required) {
            if (right - left + 1 < minLen) {
                minLen = right - left + 1;
                minStart = left;
            }
            const leftChar = s[left];
            windowMap.set(leftChar, windowMap.get(leftChar)! - 1);
            if (targetMap.has(leftChar) && windowMap.get(leftChar)! < targetMap.get(leftChar)!) formed--;
            left++;
        }
        right++;
    }

    return minLen === Infinity ? "" : s.substring(minStart, minStart + minLen);
}
```
