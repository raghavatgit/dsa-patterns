# Problem: Decode Ways

## Problem Statement
A message containing letters from A-Z can be encoded into numbers using the mapping: 'A' -> "1", ..., 'Z' -> "26". Given a string `s` containing only digits, return the number of ways to decode it.

## Intuition & Approach
Space-Optimized Dynamic Programming:
1. Let `dp[i]` be ways to decode prefix `s[0..i]`.
2. A digit at index $i$ can be decoded as a single character if $s[i] \in ['1', '9']$.
3. Two digits $s[i-1..i]$ can be decoded together if the numeric value is between 10 and 26.
4. Recurrence:
   `ways = (single_valid ? prev1 : 0) + (double_valid ? prev2 : 0)`
5. We only need the last two values (`prev1`, `prev2`), reducing memory from $O(N)$ to $O(1)$.
6. Time Complexity: $O(N)$ single pass. Space Complexity: $O(1)$ variables.

## TypeScript Implementation

```typescript
export function numDecodings(s: string): number {
  if (!s || s[0] === "0") return 0;

  const n = s.length;
  let prev2 = 1;
  let prev1 = 1;

  for (let i = 1; i < n; i++) {
    let curr = 0;
    const single = Number(s[i]);
    const double = Number(s.substring(i - 1, i + 1));

    if (single >= 1 && single <= 9) {
      curr += prev1;
    }
    if (double >= 10 && double <= 26) {
      curr += prev2;
    }

    prev2 = prev1;
    prev1 = curr;
  }

  return prev1;
}
```
