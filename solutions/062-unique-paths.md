# Problem: Unique Paths

## Problem Statement
There is a robot on an `m x n` grid. The robot is initially located at the top-left corner and tries to move to the bottom-right corner. The robot can only move either down or right at any point in time. Given the two integers `m` and `n`, return the number of possible unique paths.

## Intuition & Approach
Combinatorial Closed-Form ($O(\min(M, N))$ Time, $O(1)$ Space):
1. The robot must make exactly $m - 1$ down moves and $n - 1$ right moves, totaling $N = (m - 1) + (n - 1)$ steps.
2. The number of unique paths is equivalent to choosing $m - 1$ down steps out of $N$ total steps:
   $$\binom{m + n - 2}{m - 1} = \frac{(m + n - 2)!}{(m - 1)! (n - 1)!}$$
3. We compute the product iteratively dividing along the way to prevent integer overflow.
4. Time Complexity: $O(\min(M, N))$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function uniquePaths(m: number, n: number): number {
  const k = Math.min(m - 1, n - 1);
  const total = m + n - 2;
  let ans = 1;

  for (let i = 1; i <= k; i++) {
    ans = (ans * (total - k + i)) / i;
  }

  return Math.round(ans);
}
```

## Rust Implementation

```rust
pub fn unique_paths(m: i32, n: i32) -> i32 {
    let k = (m - 1).min(n - 1) as i64;
    let total = (m + n - 2) as i64;
    let mut ans: i64 = 1;

    for i in 1..=k {
        ans = ans * (total - k + i) / i;
    }

    ans as i32
}
```
