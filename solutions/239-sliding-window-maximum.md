# 239. Sliding Window Maximum

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(k)

## Rust Implementation
```rust
use std::collections::VecDeque;

pub fn max_sliding_window(nums: Vec<i32>, k: i32) -> Vec<i32> {
    let k = k as usize;
    let mut deque = VecDeque::new();
    let mut res = Vec::with_capacity(nums.len() - k + 1);

    for i in 0..nums.len() {
        if let Some(&front) = deque.front() {
            if front + k <= i {
                deque.pop_front();
            }
        }

        while let Some(&back) = deque.back() {
            if nums[back] < nums[i] {
                deque.pop_back();
            } else {
                break;
            }
        }

        deque.push_back(i);

        if i >= k - 1 {
            res.push(nums[*deque.front().unwrap()]);
        }
    }

    res
}
```
