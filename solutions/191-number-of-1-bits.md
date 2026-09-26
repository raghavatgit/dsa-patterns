# 191. Number of 1 Bits

## Problem Statement
Write a function that takes the binary representation of a positive integer and returns the number of set bits (`Hamming weight`).

---

## Brian Kernighan's Algorithm
The bitwise operation `n &= (n - 1)` clears the lowest set bit in `n`. The loop executes exactly once per set bit rather than 32 fixed cycles.

---

## TypeScript Implementation

```typescript
export function hammingWeight(n: number): number {
  let count = 0;
  while (n !== 0) {
    n &= (n - 1);
    count++;
  }
  return count;
}
```

---

## Rust Implementation

```rust
pub fn hamming_weight(mut n: u32) -> i32 {
    let mut count = 0;
    while n != 0 {
        n &= n - 1;
        count += 1;
    }
    count
}
```

---

## Complexity Analysis
* **Time Complexity:** O(K) where K is the count of set bits (K <= 32).
* **Space Complexity:** O(1).
