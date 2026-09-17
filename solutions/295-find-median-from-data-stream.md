# Problem: Find Median from Data Stream

## Problem Statement
The median is the middle value in an ordered integer list. Implement the `MedianFinder` class:
* `addNum(num)`: Adds an integer `num` from the data stream.
* `findMedian()`: Returns the median of all elements so far.

## Intuition & Approach
Maintain two balanced priority heaps:
1. **Max-Heap (`small`):** Stores the smaller half of numbers.
2. **Min-Heap (`large`):** Stores the larger half of numbers.

**Balance Invariants:**
* `small.size() == large.size()` or `small.size() == large.size() + 1`.
* Every element in `small` <= every element in `large`.

## Rust Implementation

```rust
use std::cmp::Reverse;
use std::collections::BinaryHeap;

pub struct MedianFinder {
    small: BinaryHeap<i32>,               // Max-Heap: smaller half
    large: BinaryHeap<Reverse<i32>>,      // Min-Heap: larger half
}

impl MedianFinder {
    pub fn new() -> Self {
        MedianFinder {
            small: BinaryHeap::new(),
            large: BinaryHeap::new(),
        }
    }

    pub fn add_num(&mut self, num: i32) {
        self.small.push(num);

        // Ensure small <= large invariant
        if let Some(&max_small) = self.small.peek() {
            if let Some(&Reverse(min_large)) = self.large.peek() {
                if max_small > min_large {
                    let val = self.small.pop().unwrap();
                    self.large.push(Reverse(val));
                }
            }
        }

        // Maintain size balance invariant
        if self.small.len() > self.large.len() + 1 {
            let val = self.small.pop().unwrap();
            self.large.push(Reverse(val));
        } else if self.large.len() > self.small.len() {
            let Reverse(val) = self.large.pop().unwrap();
            self.small.push(val);
        }
    }

    pub fn find_median(&self) -> f64 {
        if self.small.len() > self.large.len() {
            *self.small.peek().unwrap() as f64
        } else {
            let s = *self.small.peek().unwrap() as f64;
            let Reverse(l) = *self.large.peek().unwrap();
            (s + l as f64) / 2.0
        }
    }
}
```

## Complexity Analysis
* **AddNum Time:** O(log N) heap insertion and rebalancing.
* **FindMedian Time:** O(1) top-of-heap peek.
* **Space Complexity:** O(N) space to store data stream numbers.
