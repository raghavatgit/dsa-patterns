# Problem: First Missing Positive

## Problem Statement
Given an unsorted integer array `nums`, return the smallest positive integer that is not present in `nums`. You must implement an algorithm that runs in $O(N)$ time and uses $O(1)$ auxiliary space.

## Intuition & Approach
In-Place Cyclic Sort:
1. An array of length $N$ can contain positive integers in the range $[1, N]$. If every integer in $[1, N]$ is present, the answer is $N + 1$.
2. We place each number `x` in its designated position `nums[x - 1]` whenever $1 \le x \le N$ and `nums[x - 1] != x`.
3. Swap `nums[i]` with `nums[nums[i] - 1]` until current slot holds the correct element or an out-of-range integer.
4. Second pass: scan the array from index 0 to $N - 1$. The first index `i` where `nums[i] != i + 1` identifies the answer `i + 1`.
5. Time Complexity: $O(N)$ because each element is swapped into its correct index at most once. Space Complexity: $O(1)$ in-place modification.

## TypeScript Implementation

```typescript
export function firstMissingPositive(nums: number[]): number {
  const n = nums.length;

  for (let i = 0; i < n; i++) {
    while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] !== nums[i]) {
      const correctIdx = nums[i] - 1;
      const temp = nums[i];
      nums[i] = nums[correctIdx];
      nums[correctIdx] = temp;
    }
  }

  for (let i = 0; i < n; i++) {
    if (nums[i] !== i + 1) {
      return i + 1;
    }
  }

  return n + 1;
}
```

## Rust Implementation

```rust
pub fn first_missing_positive(mut nums: Vec<i32>) -> i32 {
    let n = nums.len();

    for i in 0..n {
        while nums[i] > 0 && (nums[i] as usize) <= n {
            let target_idx = (nums[i] - 1) as usize;
            if nums[target_idx] == nums[i] {
                break;
            }
            nums.swap(i, target_idx);
        }
    }

    for i in 0..n {
        if nums[i] != (i + 1) as i32 {
            return (i + 1) as i32;
        }
    }

    (n + 1) as i32
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_first_missing_positive() {
        assert_eq!(first_missing_positive(vec![1, 2, 0]), 3);
        assert_eq!(first_missing_positive(vec![3, 4, -1, 1]), 2);
        assert_eq!(first_missing_positive(vec![7, 8, 9, 11, 12]), 1);
    }
}
```
