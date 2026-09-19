# Problem: Word Break

## Problem Statement
Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

## Intuition & Approach
1D Dynamic Programming:
1. Let `dp[i]` denote whether prefix `s[0..i]` can be segmented using dictionary words.
2. Base case: `dp[0] = true` (empty string).
3. Transitions: For each index $i$ from 1 to $N$:
   - Check all partition split points $j < i$:
   - If `dp[j] == true` and substring `s[j..i]` is in `wordDict`, set `dp[i] = true` and break inner loop early.
4. Optimization: Only check split lengths $i - j$ up to the maximum word length in `wordDict`.
5. Time Complexity: $O(N^2)$ or $O(N \times L_{\max})$. Space Complexity: $O(N)$ for DP table.

## TypeScript Implementation

```typescript
export function wordBreak(s: string, wordDict: string[]): boolean {
  const dict = new Set(wordDict);
  const n = s.length;
  const dp: boolean[] = new Array(n + 1).fill(false);
  dp[0] = true;

  let maxLen = 0;
  for (const w of wordDict) {
    maxLen = Math.max(maxLen, w.length);
  }

  for (let i = 1; i <= n; i++) {
    for (let j = Math.max(0, i - maxLen); j < i; j++) {
      if (dp[j] && dict.has(s.substring(j, i))) {
        dp[i] = true;
        break;
      }
    }
  }

  return dp[n];
}
```
