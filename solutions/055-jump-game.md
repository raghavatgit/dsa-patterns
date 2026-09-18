# Problem: Jump Game

## Problem Statement
You are given an integer array `nums`. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position. Return `true` if you can reach the last index, or `false` otherwise.

## Intuition & Approach
Greedy Maximum Reachable Boundary:
1. Maintain `max_reachable` index observed so far.
2. Iterate through index `i`. If `i > max_reachable`, current position cannot be reached: return `false`.
3. Update `max_reachable = max(max_reachable, i + nums[i])`.
4. If `max_reachable >= n - 1`, target is reachable: return `true`.
5. Time Complexity: $O(N)$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function canJump(nums: number[]): boolean {
  let maxReachable = 0;
  const n = nums.length;

  for (let i = 0; i < n; i++) {
    if (i > maxReachable) return false;
    maxReachable = Math.max(maxReachable, i + nums[i]);
    if (maxReachable >= n - 1) return true;
  }

  return true;
}
```

## Rust Implementation

```rust
pub fn can_jump(nums: Vec<i32>) -> bool {
    let mut max_reachable = 0;
    let n = nums.len();

    for (i, &val) in nums.iter().enumerate() {
        if i > max_reachable {
            return false;
        }
        max_reachable = max_reachable.max(i + val as usize);
        if max_reachable >= n - 1 {
            return true;
        }
    }

    true
}
```
