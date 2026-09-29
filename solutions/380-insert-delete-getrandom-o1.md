# 380. Insert Delete GetRandom O(1)

## Complexity
- Time Complexity: O(1) average for insert, remove, getRandom
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::collections::HashMap;

pub struct RandomizedSet {
    map: HashMap<i32, usize>,
    vals: Vec<i32>,
}

impl RandomizedSet {
    pub fn new() -> Self {
        RandomizedSet {
            map: HashMap::new(),
            vals: Vec::new(),
        }
    }

    pub fn insert(&mut self, val: i32) -> bool {
        if self.map.contains_key(&val) {
            return false;
        }
        self.map.insert(val, self.vals.len());
        self.vals.push(val);
        true
    }

    pub fn remove(&mut self, val: i32) -> bool {
        if let Some(&idx) = self.map.get(&val) {
            let last_val = *self.vals.last().unwrap();
            self.vals[idx] = last_val;
            self.map.insert(last_val, idx);
            self.vals.pop();
            self.map.remove(&val);
            true
        } else {
            false
        }
    }

    pub fn get_random(&self) -> i32 {
        let idx = (self.vals.len() as u64 % (self.vals.len() as u64)) as usize;
        self.vals[idx]
    }
}
```
