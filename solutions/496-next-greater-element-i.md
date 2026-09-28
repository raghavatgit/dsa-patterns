# 496. Next Greater Element I

## Problem Statement
The **next greater element** of some element `x` in an array is the **first greater** element that is to the right of `x` in the same array.

You are given two distinct 0-indexed integer arrays `nums1` and `nums2`, where `nums1` is a subset of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the next greater element of `nums2[j]` in `nums2`. If there is no next greater element, then the answer for this query is `-1`.

Return an array `ans` of length `nums1.length` such that `ans[i]` is the next greater element as described above.

---

## TypeScript Implementation

```typescript
export function nextGreaterElement(nums1: number[], nums2: number[]): number[] {
  const nextGreater = new Map<number, number>();
  const stack: number[] = [];

  for (const num of nums2) {
    while (stack.length > 0 && stack[stack.length - 1] < num) {
      const top = stack.pop()!;
      nextGreater.set(top, num);
    }
    stack.push(num);
  }

  return nums1.map((num) => nextGreater.get(num) ?? -1);
}
```

---

## Rust Implementation

```rust
use std::collections::HashMap;

pub struct Solution;

impl Solution {
    pub fn next_greater_element(nums1: Vec<i32>, nums2: Vec<i32>) -> Vec<i32> {
        let mut map: HashMap<i32, i32> = HashMap::with_capacity(nums2.len());
        let mut stack: Vec<i32> = Vec::new();

        for &num in &nums2 {
            while let Some(&top) = stack.last() {
                if top < num {
                    map.insert(top, num);
                    stack.pop();
                } else {
                    break;
                }
            }
            stack.push(num);
        }

        nums1.into_iter().map(|n| *map.get(&n).unwrap_or(&-1)).collect()
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(n1 + n2)` since each element of `nums2` is pushed and popped at most once.
- Space Complexity: `O(n2)` for the monotonic stack and hash map lookup table.
