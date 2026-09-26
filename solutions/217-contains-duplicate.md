# 217. Contains Duplicate

## Problem Statement
Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

---

## TypeScript Implementation

```typescript
export function containsDuplicate(nums: number[]): boolean {
  const seen = new Set<number>();
  for (const num of nums) {
    if (seen.has(num)) return true;
    seen.add(num);
  }
  return false;
}
```

---

## Rust Implementation

```rust
use std::collections::HashSet;

pub fn contains_duplicate(nums: Vec<i32>) -> bool {
    let mut seen = HashSet::with_capacity(nums.len());
    for num in nums {
        if !seen.insert(num) {
            return true;
        }
    }
    false
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) average case hash lookup.
* **Space Complexity:** O(N) hash set.
