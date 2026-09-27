# 026. Remove Duplicates from Sorted Array

## Problem Statement
Given an integer array `nums` sorted in non-decreasing order, remove duplicates in-place such that each unique element appears only once. Return the number of unique elements `k`.

---

## TypeScript Implementation

```typescript
export function removeDuplicates(nums: number[]): number {
  if (nums.length === 0) return 0;
  let write = 1;

  for (let read = 1; read < nums.length; read++) {
    if (nums[read] !== nums[write - 1]) {
      nums[write] = nums[read];
      write++;
    }
  }

  return write;
}
```

---

## Rust Implementation

```rust
pub fn remove_duplicates(nums: &mut Vec<i32>) -> i32 {
    if nums.is_empty() {
        return 0;
    }

    let mut write = 1;
    for read in 1..nums.len() {
        if nums[read] != nums[write - 1] {
            nums[write] = nums[read];
            write += 1;
        }
    }

    write as i32
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) single pass.
* **Space Complexity:** O(1) in-place modification.
