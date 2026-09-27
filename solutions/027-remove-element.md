# 027. Remove Element

## Problem Statement
Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` in-place. The order of elements may be changed. Then return the number of elements in `nums` which are not equal to `val`.

---

## TypeScript Implementation

```typescript
export function removeElement(nums: number[], val: number): number {
  let write = 0;
  for (let read = 0; read < nums.length; read++) {
    if (nums[read] !== val) {
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
pub fn remove_element(nums: &mut Vec<i32>, val: i32) -> i32 {
    let mut write = 0;
    for read in 0..nums.len() {
        if nums[read] != val {
            nums[write] = nums[read];
            write += 1;
        }
    }
    write as i32
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N) linear scan.
* **Space Complexity:** O(1) in-place.
