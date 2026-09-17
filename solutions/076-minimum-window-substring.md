# Problem: Minimum Window Substring

## Problem Statement
Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.

## Intuition & Approach
Sliding Window with Frequency Map:
1. Build a frequency table `target_counts` for string `t` and track required unique characters `required = len(target_counts)`.
2. Expand the right window pointer `r` one character at a time. If the character matches a target count, decrement required balance.
3. Once all characters are satisfied (`formed == required`), contract the left window pointer `l` to minimize window length while preserving validity.
4. Record minimal window start and length.
5. Time Complexity: $O(M + N)$ where each character is visited at most twice. Space Complexity: $O(K)$ where $K$ is character alphabet size.

## TypeScript Implementation

```typescript
export function minWindow(s: string, t: string): string {
  if (s.length === 0 || t.length === 0) return "";

  const targetMap = new Map<string, number>();
  for (const ch of t) {
    targetMap.set(ch, (targetMap.get(ch) || 0) + 1);
  }

  const windowMap = new Map<string, number>();
  let required = targetMap.size;
  let formed = 0;

  let minLen = Infinity;
  let minStart = 0;
  let l = 0;

  for (let r = 0; r < s.length; r++) {
    const ch = s[r];
    windowMap.set(ch, (windowMap.get(ch) || 0) + 1);

    if (targetMap.has(ch) && windowMap.get(ch) === targetMap.get(ch)) {
      formed++;
    }

    while (l <= r && formed === required) {
      if (r - l + 1 < minLen) {
        minLen = r - l + 1;
        minStart = l;
      }

      const leftChar = s[l];
      windowMap.set(leftChar, windowMap.get(leftChar)! - 1);
      if (targetMap.has(leftChar) && windowMap.get(leftChar)! < targetMap.get(leftChar)!) {
        formed--;
      }
      l++;
    }
  }

  return minLen === Infinity ? "" : s.substring(minStart, minStart + minLen);
}
```
