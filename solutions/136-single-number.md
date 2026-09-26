# 136. Single Number

## Problem Statement
Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one. Implement a solution with linear runtime and constant space.

---

## Bitwise XOR Invariants
1. `x ^ x = 0` (Self-cancellation)
2. `x ^ 0 = x` (Identity)
3. XOR is associative and commutative. Cumulative XOR cancels all pairs, isolating the single element.

---

## TypeScript Implementation

```typescript
export function singleNumber(nums: number[]): number {
  let acc = 0;
  for (const num of nums) acc ^= num;
  return acc;
}
```

---

## Rust Implementation

```rust
pub fn single_number(nums: Vec<i32>) -> i32 {
    nums.into_iter().fold(0, |acc, x| acc ^ x)
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) single pass.
* **Space Complexity:** O(1) constant auxiliary space.
