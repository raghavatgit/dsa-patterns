# 347. Top K Frequent Elements

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::collections::HashMap;

pub fn top_k_frequent(nums: Vec<i32>, k: i32) -> Vec<i32> {
    let mut counts = HashMap::new();
    for x in nums.iter() {
        *counts.entry(*x).or_insert(0) += 1;
    }

    let mut buckets: Vec<Vec<i32>> = vec![Vec::new(); nums.len() + 1];
    for (&val, &count) in counts.iter() {
        buckets[count].push(val);
    }

    let mut res = Vec::new();
    let k = k as usize;

    for i in (0..=nums.len()).rev() {
        for &val in &buckets[i] {
            res.push(val);
            if res.len() == k {
                return res;
            }
        }
    }

    res
}
```
