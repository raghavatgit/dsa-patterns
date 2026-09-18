# Problem: Sliding Window Maximum

## Problem Statement
You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

## Intuition & Approach
Monotonic Decreasing Deque:
1. Maintain a double-ended queue (`deque`) storing indices of elements in descending order of value.
2. For each element `nums[i]`:
   - Evict indices from the front that fall outside the active window boundary: `deque.front() <= i - k`.
   - Evict indices from the back whose corresponding values are less than or equal to `nums[i]` (they can never be the maximum of this or future windows).
   - Push current index `i` to the back.
3. Once `i >= k - 1`, the maximum element of the current window is guaranteed to be at `deque.front()`.
4. Time Complexity: Strict $O(N)$ as each index is pushed and popped at most once. Space Complexity: $O(K)$ deque storage.

## TypeScript Implementation

```typescript
export function maxSlidingWindow(nums: number[], k: number): number[] {
  const n = nums.length;
  if (n === 0 || k === 0) return [];

  const deque: number[] = [];
  const result: number[] = [];

  for (let i = 0; i < n; i++) {
    // Remove indices outside active window
    if (deque.length > 0 && deque[0] <= i - k) {
      deque.shift();
    }

    // Maintain monotonic decreasing order
    while (deque.length > 0 && nums[deque[deque.length - 1]] <= nums[i]) {
      deque.pop();
    }

    deque.push(i);

    // Record maximum once first window of size k is formed
    if (i >= k - 1) {
      result.push(nums[deque[0]]);
    }
  }

  return result;
}
```

## Rust Implementation

```rust
use std::collections::VecDeque;

pub fn max_sliding_window(nums: Vec<i32>, k: i32) -> Vec<i32> {
    let k = k as usize;
    let n = nums.len();
    if n == 0 || k == 0 { return vec![]; }

    let mut deque = VecDeque::new();
    let mut result = Vec::with_capacity(n - k + 1);

    for i in 0..n {
        if let Some(&front) = deque.front() {
            if front + k <= i {
                deque.pop_front();
            }
        }

        while let Some(&back) = deque.back() {
            if nums[back] <= nums[i] {
                deque.pop_back();
            } else {
                break;
            }
        }

        deque.push_back(i);

        if i + 1 >= k {
            result.push(nums[*deque.front().unwrap()]);
        }
    }

    result
}
```
