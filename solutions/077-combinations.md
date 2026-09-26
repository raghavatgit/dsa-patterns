# 077. Combinations

## Problem Statement
Given two integers `n` and `k`, return all possible combinations of `k` numbers chosen from the range `[1, n]`.

---

## Pruning Invariant
At iteration `i`, if `k - path.length > n - i + 1`, there are not enough remaining elements to complete a valid combination. Terminate the branch early.

---

## TypeScript Implementation

```typescript
export function combine(n: number, k: number): number[][] {
  const result: number[][] = [];
  const current: number[] = [];

  function backtrack(start: number) {
    if (current.length === k) {
      result.push([...current]);
      return;
    }

    // Prune invalid branches
    const needed = k - current.length;
    for (let i = start; i <= n - needed + 1; i++) {
      current.push(i);
      backtrack(i + 1);
      current.pop();
    }
  }

  backtrack(1);
  return result;
}
```

---

## Rust Implementation

```rust
pub fn combine(n: i32, k: i32) -> Vec<Vec<i32>> {
    let mut result = Vec::new();
    let mut current = Vec::with_capacity(k as usize);

    fn backtrack(start: i32, n: i32, k: i32, current: &mut Vec<i32>, result: &mut Vec<Vec<i32>>) {
        if current.len() == k as usize {
            result.push(current.clone());
            return;
        }

        let needed = k as usize - current.len();
        let upper_bound = n as usize - needed + 1;

        for i in start..=(upper_bound as i32) {
            current.push(i);
            backtrack(i + 1, n, k, current, result);
            current.pop();
        }
    }

    backtrack(1, n, k, &mut current, &mut result);
    result
}
```

---

## Complexity Analysis
* **Time Complexity:** O(k * C(n, k)) generating each combination.
* **Space Complexity:** O(k) recursion stack depth.
