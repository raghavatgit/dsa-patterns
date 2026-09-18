# Problem: Jump Game II

## Problem Statement
You are given a 0-indexed array of integers `nums` of length `n`. You are initially positioned at `nums[0]`. Each element `nums[i]` represents the maximum length of a forward jump from index `i`. Return the minimum number of jumps to reach `nums[n - 1]`.

## Intuition & Approach
Greedy Range Expansion (Implicit BFS):
1. Maintain current jump window `[curr_start, curr_end]`.
2. Determine `farthest` reachable index from any position within the current window: `farthest = max(farthest, i + nums[i])`.
3. Once iteration reaches `curr_end`:
   - We must take another jump: `jumps++`.
   - Update window boundaries: `curr_end = farthest`.
   - If `curr_end >= n - 1`, we can reach or exceed the destination.
4. Time Complexity: $O(N)$ single pass. Space Complexity: $O(1)$ auxiliary variables.

## TypeScript Implementation

```typescript
export function jump(nums: number[]): number {
  const n = nums.length;
  if (n <= 1) return 0;

  let jumps = 0;
  let currEnd = 0;
  let farthest = 0;

  for (let i = 0; i < n - 1; i++) {
    farthest = Math.max(farthest, i + nums[i]);

    if (i === currEnd) {
      jumps++;
      currEnd = farthest;
      if (currEnd >= n - 1) break;
    }
  }

  return jumps;
}
```

## Rust Implementation

```rust
pub fn jump(nums: Vec<i32>) -> i32 {
    let n = nums.len();
    if n <= 1 { return 0; }

    let mut jumps = 0;
    let mut curr_end = 0;
    let mut farthest = 0;

    for i in 0..(n - 1) {
        farthest = farthest.max(i + nums[i] as usize);

        if i == curr_end {
            jumps += 1;
            curr_end = farthest;
            if curr_end >= n - 1 {
                break;
            }
        }
    }

    jumps
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_jump() {
        assert_eq!(jump(vec![2, 3, 1, 1, 4]), 2);
        assert_eq!(jump(vec![2, 3, 0, 1, 4]), 2);
    }
}
```
