# 703. Kth Largest Element in a Stream

## Complexity
- Time Complexity: O(log k) per add
- Space Complexity: O(k)

## Rust Implementation
```rust
use std::collections::BinaryHeap;
use std::cmp::Reverse;

pub struct KthLargest {
    k: usize,
    heap: BinaryHeap<Reverse<i32>>,
}

impl KthLargest {
    pub fn new(k: i32, nums: Vec<i32>) -> Self {
        let mut obj = KthLargest {
            k: k as usize,
            heap: BinaryHeap::new(),
        };
        for n in nums {
            obj.add(n);
        }
        obj
    }

    pub fn add(&mut self, val: i32) -> i32 {
        self.heap.push(Reverse(val));
        if self.heap.len() > self.k {
            self.heap.pop();
        }
        self.heap.peek().unwrap().0
    }
}
```
