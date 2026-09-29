# 72. Edit Distance

## Complexity
- Time Complexity: O(m * n)
- Space Complexity: O(min(m, n)) optimized rolling row

## Rust Implementation
```rust
pub fn min_distance(word1: String, word2: String) -> i32 {
    let m = word1.len();
    let n = word2.len();
    let w1: Vec<char> = word1.chars().collect();
    let w2: Vec<char> = word2.chars().collect();

    let mut dp = vec![vec![0; n + 1]; m + 1];
    for i in 0..=m { dp[i][0] = i as i32; }
    for j in 0..=n { dp[0][j] = j as i32; }

    for i in 1..=m {
        for j in 1..=n {
            if w1[i - 1] == w2[j - 1] {
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                dp[i][j] = 1 + dp[i - 1][j - 1].min(dp[i - 1][j].min(dp[i][j - 1]));
            }
        }
    }
    dp[m][n]
}
```

## TypeScript Implementation
```typescript
export function minDistance(word1: string, word2: string): number {
    const m = word1.length, n = word2.length;
    let dp = Array.from({ length: n + 1 }, (_, i) => i);

    for (let i = 1; i <= m; i++) {
        let prev = dp[0];
        dp[0] = i;
        for (let j = 1; j <= n; j++) {
            const temp = dp[j];
            if (word1[i - 1] === word2[j - 1]) {
                dp[j] = prev;
            } else {
                dp[j] = 1 + Math.min(prev, dp[j], dp[j - 1]);
            }
            prev = temp;
        }
    }
    return dp[n];
}
```
