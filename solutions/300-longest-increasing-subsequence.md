# Problem: Longest Increasing Subsequence (LIS)

## Problem Statement
Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

## Intuition & Approach
* **Dynamic Programming:** $O(N^2)$ checks all predecessors.
* **Patience Sorting + Binary Search:** $O(N \log N)$. Maintain an array `tails` where `tails[i]` stores the smallest tail of all increasing subsequences of length `i + 1`:
  * For each `x` in `nums`, binary search for `x` in `tails`.
  * If `x` is larger than all elements, append `x` to `tails`.
  * Otherwise, replace the first element `>= x` with `x`.
  * Length of `tails` equals the LIS.

## TypeScript Implementation

```typescript
export function lengthOfLIS(nums: number[]): number {
  if (nums.length === 0) return 0;

  const tails: number[] = [];

  for (const num of nums) {
    let left = 0;
    let right = tails.length;

    // Binary search for insertion index
    while (left < right) {
      const mid = Math.floor((left + right) / 2);
      if (tails[mid] < num) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }

    if (left === tails.length) {
      tails.push(num);
    } else {
      tails[left] = num;
    }
  }

  return tails.length;
}
```

## Rust Implementation

```rust
pub fn length_of_lis(nums: &[i32]) -> i32 {
    let mut tails = Vec::with_capacity(nums.len());

    for &num in nums {
        match tails.binary_search(&num) {
            Ok(_) => {}, // Duplicate does not extend strictly increasing subsequence
            Err(idx) => {
                if idx == tails.len() {
                    tails.push(num);
                } else {
                    tails[idx] = num;
                }
            }
        }
    }

    tails.len() as i32
}
```

## Complexity Analysis
* **Time Complexity:** O(N log N) binary search for each of the N elements.
* **Space Complexity:** O(N) auxiliary space for the tails buffer.
