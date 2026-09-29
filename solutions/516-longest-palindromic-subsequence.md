# 516. Longest Palindromic Subsequence

## Complexity
- Time Complexity: O(n^2)
- Space Complexity: O(n^2)

## Rust Implementation
```rust
pub fn longest_palindrome_subseq(s: String) -> i32 {
    let bytes = s.as_bytes();
    let n = bytes.len();
    let mut dp = vec![vec![0; n]; n];
    for i in (0..n).rev() {
        dp[i][i] = 1;
        for j in (i + 1)..n {
            if bytes[i] == bytes[j] {
                dp[i][j] = dp[i + 1][j - 1] + 2;
            } else {
                dp[i][j] = dp[i + 1][j].max(dp[i][j - 1]);
            }
        }
    }
    dp[0][n - 1]
}
```

## TypeScript Implementation
```typescript
export function longestPalindromeSubseq(s: string): number {
    const n = s.length;
    const dp = Array.from({ length: n }, () => new Array(n).fill(0));
    for (let i = n - 1; i >= 0; i--) {
        dp[i][i] = 1;
        for (let j = i + 1; j < n; j++) {
            if (s[i] === s[j]) {
                dp[i][j] = dp[i + 1][j - 1] + 2;
            } else {
                dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
            }
        }
    }
    return dp[0][n - 1];
}
```
