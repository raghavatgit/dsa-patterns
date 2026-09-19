# Problem: Climbing Stairs

## Problem Statement
You are climbing a staircase. It takes `n` steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

## Intuition & Approach
Matrix Exponentiation ($O(\log N)$ Time):
1. The recurrence follows Fibonacci: $f(n) = f(n - 1) + f(n - 2)$ with $f(1) = 1, f(2) = 2$.
2. In matrix form:
   $$\begin{pmatrix} f(n) \\ f(n - 1) \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}^{n - 1} \begin{pmatrix} f(1) \\ f(0) \end{pmatrix}$$
3. Using binary exponentiation, matrix power $M^{n - 1}$ is computed in $O(\log N)$ multiplications.
4. Time Complexity: $O(\log N)$ matrix exponentiation or $O(N)$ iterative loop. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function climbStairs(n: number): number {
  if (n <= 2) return n;

  let prev2 = 1;
  let prev1 = 2;

  for (let i = 3; i <= n; i++) {
    const curr = prev1 + prev2;
    prev2 = prev1;
    prev1 = curr;
  }

  return prev1;
}
```

## Rust Implementation

```rust
pub fn climb_stairs(n: i32) -> i32 {
    if n <= 2 { return n; }

    let mut prev2 = 1;
    let mut prev1 = 2;

    for _ in 3..=n {
        let curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }

    prev1
}
```
