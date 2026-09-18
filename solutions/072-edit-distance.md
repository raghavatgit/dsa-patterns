# Problem: Edit Distance (Levenshtein Distance)

## Problem Statement
Given two strings `word1` and `word2`, return the minimum number of operations required to convert `word1` to `word2`. You have the following three operations permitted on a word:
- Insert a character
- Delete a character
- Replace a character

## Intuition & Approach
Dynamic Programming with Space Optimization:
1. Let `dp[i][j]` denote the minimum edit distance to transform prefix `word1[0..i]` into `word2[0..j]`.
2. Base cases:
   - `dp[0][j] = j` (insert $j$ characters)
   - `dp[i][0] = i` (delete $i$ characters)
3. Transitions:
   - If `word1[i - 1] == word2[j - 1]`: `dp[i][j] = dp[i - 1][j - 1]`
   - Otherwise: `dp[i][j] = 1 + min(dp[i - 1][j] (delete), dp[i][j - 1] (insert), dp[i - 1][j - 1] (replace))`
4. Space Optimization: Since row `i` depends exclusively on row `i - 1`, we reduce memory from $O(M \times N)$ to a single 1D array of size $O(N)$ with a `prev_diagonal` scalar.
5. Time Complexity: $O(M \times N)$. Space Complexity: $O(N)$ auxiliary storage.

## TypeScript Implementation

```typescript
export function minDistance(word1: string, word2: string): number {
  const m = word1.length;
  const n = word2.length;

  const dp: number[] = Array.from({ length: n + 1 }, (_, j) => j);

  for (let i = 1; i <= m; i++) {
    let prev = dp[0];
    dp[0] = i;

    for (let j = 1; j <= n; j++) {
      const temp = dp[j];
      if (word1[i - 1] === word2[j - 1]) {
        dp[j] = prev;
      } else {
        dp[j] = 1 + Math.min(dp[j], dp[j - 1], prev);
      }
      prev = temp;
    }
  }

  return dp[n];
}
```

## Rust Implementation

```rust
pub fn min_distance(word1: String, word2: String) -> i32 {
    let w1: Vec<char> = word1.chars().collect();
    let w2: Vec<char> = word2.chars().collect();
    let m = w1.len();
    let n = w2.len();

    let mut dp: Vec<i32> = (0..=n as i32).collect();

    for i in 1..=m {
        let mut prev = dp[0];
        dp[0] = i as i32;

        for j in 1..=n {
            let temp = dp[j];
            if w1[i - 1] == w2[j - 1] {
                dp[j] = prev;
            } else {
                dp[j] = 1 + dp[j].min(dp[j - 1]).min(prev);
            }
            prev = temp;
        }
    }

    dp[n]
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_min_distance() {
        assert_eq!(min_distance("horse".to_string(), "ros".to_string()), 3);
        assert_eq!(min_distance("intention".to_string(), "execution".to_string()), 5);
    }
}
```
