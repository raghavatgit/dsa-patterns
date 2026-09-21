# Problem: Letter Combinations of a Phone Number

## Problem Statement
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

## Intuition & Approach
Iterative BFS / Cartesian Product:
1. Map each digit to its corresponding keypad letters.
2. Initialize queue with empty string `[""]`.
3. For each digit:
   - Pop existing strings from previous step.
   - For each string, append each letter of the current digit.
4. Time Complexity: $O(4^N \times N)$. Space Complexity: $O(4^N \times N)$.

## TypeScript Implementation

```typescript
export function letterCombinations(digits: string): string[] {
  if (!digits || digits.length === 0) return [];

  const phoneMap: Record<string, string[]> = {
    "2": ["a", "b", "c"],
    "3": ["d", "e", "f"],
    "4": ["g", "h", "i"],
    "5": ["j", "k", "l"],
    "6": ["m", "n", "o"],
    "7": ["p", "q", "r", "s"],
    "8": ["t", "u", "v"],
    "9": ["w", "x", "y", "z"]
  };

  let combinations: string[] = [""];

  for (const digit of digits) {
    const letters = phoneMap[digit] || [];
    const nextLevel: string[] = [];

    for (const prefix of combinations) {
      for (const ch of letters) {
        nextLevel.push(prefix + ch);
      }
    }

    combinations = nextLevel;
  }

  return combinations;
}
```
