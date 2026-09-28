# 215. Kth Largest Element in an Array

## Complexity
- Time Complexity: O(n log k)
- Space Complexity: O(k)

## Rust Implementation
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

pub fn find_kth_largest(nums: Vec<i32>, k: i32) -> i32 {
    let mut min_heap = BinaryHeap::new();
    let k = k as usize;

    for num in nums {
        min_heap.push(Reverse(num));
        if min_heap.len() > k {
            min_heap.pop();
        }
    }

    min_heap.peek().unwrap().0
}
```
