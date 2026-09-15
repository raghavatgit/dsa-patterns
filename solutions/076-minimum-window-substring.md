# Problem: Minimum Window Substring

## Problem Statement
Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return `""`.

## Intuition & Approach
Use dynamic sliding window with two pointers `left` and `right`:
1. Build frequency map of target string `t`.
2. Expand `right` pointer, decrementing character frequencies. When all characters are satisfied (`matched == required`), contract `left` pointer to minimize the valid window.
3. Track minimum length and starting index throughout contraction.

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

  let left = 0;
  let minLen = Infinity;
  let minStart = 0;

  for (let right = 0; right < s.length; right++) {
    const ch = s[right];
    windowMap.set(ch, (windowMap.get(ch) || 0) + 1);

    if (targetMap.has(ch) && windowMap.get(ch) === targetMap.get(ch)) {
      formed++;
    }

    while (left <= right && formed === required) {
      if (right - left + 1 < minLen) {
        minLen = right - left + 1;
        minStart = left;
      }

      const leftChar = s[left];
      windowMap.set(leftChar, windowMap.get(leftChar)! - 1);
      if (targetMap.has(leftChar) && windowMap.get(leftChar)! < targetMap.get(leftChar)!) {
        formed--;
      }
      left++;
    }
  }

  return minLen === Infinity ? "" : s.substring(minStart, minStart + minLen);
}
```

## Complexity Analysis
* **Time Complexity:** O(M + N) where each character in `s` is visited at most twice (by `left` and `right`).
* **Space Complexity:** O(ALPHA) auxiliary space bounded by distinct alphabet characters.
