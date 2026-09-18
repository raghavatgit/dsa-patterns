# Problem: Regular Expression Matching

## Problem Statement
Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:
- `'.'` Matches any single character.
- `'*'` Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).

## Intuition & Approach
2D Dynamic Programming with Subproblem Memoization:
1. Let `dp[i][j]` represent whether prefix `s[0..i]` matches pattern prefix `p[0..j]`.
2. Base case: `dp[0][0] = true` (empty string matches empty pattern).
3. Transitions:
   - If `p[j - 1] != '*'`: Characters must match directly:
     `dp[i][j] = dp[i - 1][j - 1] && (s[i - 1] == p[j - 1] || p[j - 1] == '.')`
   - If `p[j - 1] == '*'`:
     - Case 1 (0 occurrences): Ignore `*` and its predecessor: `dp[i][j] = dp[i][j - 2]`
     - Case 2 (1+ occurrences): Preceding character matches current character `s[i - 1]`:
       `dp[i][j] = dp[i][j] || (dp[i - 1][j] && (s[i - 1] == p[j - 2] || p[j - 2] == '.'))`
4. Time Complexity: $O(M \times N)$ where $M = \text{len}(s)$ and $N = \text{len}(p)$. Space Complexity: $O(M \times N)$.

## TypeScript Implementation

```typescript
export function isMatch(s: string, p: string): boolean {
  const m = s.length;
  const n = p.length;
  const dp: boolean[][] = Array.from({ length: m + 1 }, () => new Array(n + 1).fill(false));

  dp[0][0] = true;

  // Patterns like a*, a*b*, a*b*c* can match empty string
  for (let j = 2; j <= n; j += 2) {
    if (p[j - 1] === "*") {
      dp[0][j] = dp[0][j - 2];
    }
  }

  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      if (p[j - 1] === "*") {
        const noMatch = dp[i][j - 2];
        const charMatch = s[i - 1] === p[j - 2] || p[j - 2] === ".";
        dp[i][j] = noMatch || (charMatch && dp[i - 1][j]);
      } else {
        const charMatch = s[i - 1] === p[j - 1] || p[j - 1] === ".";
        dp[i][j] = charMatch && dp[i - 1][j - 1];
      }
    }
  }

  return dp[m][n];
}
```

## Rust Implementation

```rust
pub fn is_match(s: String, p: String) -> bool {
    let s_chars: Vec<char> = s.chars().collect();
    let p_chars: Vec<char> = p.chars().collect();
    let m = s_chars.len();
    let n = p_chars.len();

    let mut dp = vec![vec![false; n + 1]; m + 1];
    dp[0][0] = true;

    for j in 2..=n {
        if p_chars[j - 1] == '*' {
            dp[0][j] = dp[0][j - 2];
        }
    }

    for i in 1..=m {
        for j in 1..=n {
            if p_chars[j - 1] == '*' {
                let zero_match = dp[i][j - 2];
                let char_match = s_chars[i - 1] == p_chars[j - 2] || p_chars[j - 2] == '.';
                dp[i][j] = zero_match || (char_match && dp[i - 1][j]);
            } else {
                let char_match = s_chars[i - 1] == p_chars[j - 1] || p_chars[j - 1] == '.';
                dp[i][j] = char_match && dp[i - 1][j - 1];
            }
        }
    }

    dp[m][n]
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_regex_matching() {
        assert_eq!(is_match("aa".to_string(), "a".to_string()), false);
        assert_eq!(is_match("aa".to_string(), "a*".to_string()), true);
        assert_eq!(is_match("ab".to_string(), ".*".to_string()), true);
    }
}
```
