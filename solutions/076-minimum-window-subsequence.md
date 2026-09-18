# Problem: Minimum Window Subsequence

## Problem Statement
Given strings `s1` and `s2`, return the minimum contiguous substring `W` of `s1`, so that `s2` is a subsequence of `W`. If there is no such window in `s1` that covers all characters in `s2`, return the empty string `""`. If there are multiple minimum-length windows, return the one with the smallest starting index.

## Intuition & Approach
Two-Pointer Forward Match and Backward Contraction:
1. Scan forward matching characters of `s2` in `s1`.
2. Once the final character of `s2` is matched at index `s1_end`:
   - Scan backwards from `s1_end` matching characters of `s2` in reverse.
   - This pinpoints the largest possible starting index `s1_start` that yields the tightest valid window ending at `s1_end`.
3. Record window if shorter than previously observed minimum.
4. Advance search pointer to `s1_start + 1` to find subsequent windows.
5. Time Complexity: $O(M \times N)$ worst case, where $M = \text{len}(s1)$ and $N = \text{len}(s2)$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function minWindowSubsequence(s1: string, s2: string): string {
  let m = s1.length;
  let n = s2.length;
  let s1Idx = 0;
  let s2Idx = 0;
  let minLen = Infinity;
  let startIdx = -1;

  while (s1Idx < m) {
    if (s1[s1Idx] === s2[s2Idx]) {
      s2Idx++;
      if (s2Idx === n) {
        // Complete match formed; contract backwards
        let end = s1Idx;
        s2Idx--;
        while (s2Idx >= 0) {
          if (s1[s1Idx] === s2[s2Idx]) {
            s2Idx--;
          }
          s1Idx--;
        }
        s1Idx++;
        s2Idx = 0;

        const currentLen = end - s1Idx + 1;
        if (currentLen < minLen) {
          minLen = currentLen;
          startIdx = s1Idx;
        }
      }
    }
    s1Idx++;
  }

  return startIdx === -1 ? "" : s1.substring(startIdx, startIdx + minLen);
}
```
