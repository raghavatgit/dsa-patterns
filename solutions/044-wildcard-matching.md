# Problem: Wildcard Matching

## Problem Statement
Given an input string `s` and a pattern `p`, implement wildcard pattern matching with support for `'?'` and `'*'` where:
- `'?'` Matches any single character.
- `'*'` Matches any sequence of characters (including the empty sequence).
The matching should cover the entire input string.

## Intuition & Approach
Two-Pointer Greedy Backtracking with Star Checkpoint:
1. Maintain pointers `s_idx` in `s` and `p_idx` in `p`.
2. When characters match or `p[p_idx] == '?'`, advance both pointers.
3. When `p[p_idx] == '*'`: Record checkpoints `star_idx = p_idx` and `match_idx = s_idx`, then greedily advance `p_idx`.
4. When characters mismatch:
   - If a preceding `*` was recorded, backtrack: increment `match_idx`, reset `s_idx = match_idx`, and set `p_idx = star_idx + 1`.
   - If no preceding `*` exists, matching fails.
5. Skip remaining trailing `*` in pattern.
6. Time Complexity: $O(M \times N)$ worst-case, $O(N)$ average time. Space Complexity: $O(1)$ auxiliary memory.

## TypeScript Implementation

```typescript
export function isMatchWildcard(s: string, p: string): boolean {
  let sIdx = 0;
  let pIdx = 0;
  let starIdx = -1;
  let matchIdx = 0;

  while (sIdx < s.length) {
    if (pIdx < p.length && (p[pIdx] === "?" || p[pIdx] === s[sIdx])) {
      sIdx++;
      pIdx++;
    } else if (pIdx < p.length && p[pIdx] === "*") {
      starIdx = pIdx;
      matchIdx = sIdx;
      pIdx++;
    } else if (starIdx !== -1) {
      pIdx = starIdx + 1;
      matchIdx++;
      sIdx = matchIdx;
    } else {
      return false;
    }
  }

  while (pIdx < p.length && p[pIdx] === "*") {
    pIdx++;
  }

  return pIdx === p.length;
}
```
