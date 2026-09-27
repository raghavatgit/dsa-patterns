# 066. Plus One

## Problem Statement
You are given a large integer represented as an integer array `digits`. Increment the large integer by one and return the resulting array of digits.

---

## TypeScript Implementation

```typescript
export function plusOne(digits: number[]): number[] {
  for (let i = digits.length - 1; i >= 0; i--) {
    if (digits[i] < 9) {
      digits[i]++;
      return digits;
    }
    digits[i] = 0;
  }

  return [1, ...digits];
}
```

---

## Rust Implementation

```rust
pub fn plus_one(mut digits: Vec<i32>) -> Vec<i32> {
    for i in (0..digits.len()).rev() {
        if digits[i] < 9 {
            digits[i] += 1;
            return digits;
        }
        digits[i] = 0;
    }

    let mut result = vec![1];
    result.extend(digits);
    result
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) worst case all 9s.
* **Space Complexity:** O(1) in-place unless all 9s.
