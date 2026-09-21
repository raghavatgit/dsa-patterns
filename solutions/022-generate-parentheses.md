# Problem: Generate Parentheses

## Problem Statement
Given `n` pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

## Intuition & Approach
Balanced Bracket Backtracking:
1. Maintain counts `open` and `close`.
2. Base case: If `current.length == 2 * n`, valid combination reached.
3. Invariant 1: Can append `'('` whenever `open < n`.
4. Invariant 2: Can append `')'` only when `close < open` (ensuring well-formed prefix).
5. Number of valid combinations is the Catalan number $C_n = \frac{1}{n+1} \binom{2n}{n}$.
6. Time Complexity: $O(\frac{4^n}{\sqrt{n}})$. Space Complexity: $O(N)$ recursion depth.

## TypeScript Implementation

```typescript
export function generateParenthesis(n: number): string[] {
  const results: string[] = [];

  function backtrack(curr: string, open: number, close: number) {
    if (curr.length === 2 * n) {
      results.push(curr);
      return;
    }

    if (open < n) {
      backtrack(curr + "(", open + 1, close);
    }
    if (close < open) {
      backtrack(curr + ")", open, close + 1);
    }
  }

  backtrack("", 0, 0);
  return results;
}
```

## Rust Implementation

```rust
pub fn generate_parenthesis(n: i32) -> Vec<String> {
    let mut results = Vec::new();
    let mut curr = String::with_capacity(2 * n as usize);

    fn backtrack(open: i32, close: i32, n: i32, curr: &mut String, results: &mut Vec<String>) {
        if curr.len() == (2 * n) as usize {
            results.push(curr.clone());
            return;
        }

        if open < n {
            curr.push('(');
            backtrack(open + 1, close, n, curr, results);
            curr.pop();
        }
        if close < open {
            curr.push(')');
            backtrack(open, close + 1, n, curr, results);
            curr.pop();
        }
    }

    backtrack(0, 0, n, &mut curr, &mut results);
    results
}
```
