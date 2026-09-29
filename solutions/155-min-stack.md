# 155. Min Stack

## Complexity
- Time Complexity: O(1) for push, pop, top, getMin
- Space Complexity: O(n)

## Rust Implementation
```rust
pub struct MinStack {
    stack: Vec<i32>,
    min_stack: Vec<i32>,
}

impl MinStack {
    pub fn new() -> Self {
        MinStack { stack: Vec::new(), min_stack: Vec::new() }
    }

    pub fn push(&mut self, val: i32) {
        self.stack.push(val);
        let min_val = match self.min_stack.last() {
            Some(&curr_min) => std::cmp::min(curr_min, val),
            None => val,
        };
        self.min_stack.push(min_val);
    }

    pub fn pop(&mut self) {
        self.stack.pop();
        self.min_stack.pop();
    }

    pub fn top(&self) -> i32 {
        *self.stack.last().unwrap()
    }

    pub fn get_min(&self) -> i32 {
        *self.min_stack.last().unwrap()
    }
}
```
