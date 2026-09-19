# Problem: Min Stack

## Problem Statement
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time. Implement the `MinStack` class with `push(val)`, `pop()`, `top()`, and `getMin()` in $O(1)$ time.

## Intuition & Approach
Paired Value/Min Stack:
1. Each entry in the stack stores a pair: `(value, minimum_at_or_below)`.
2. When pushing `val`, new minimum is `min(val, current_min)`.
3. When popping, previous minimum is automatically restored with zero lookups.
4. Time Complexity: Strict $O(1)$ for all operations. Space Complexity: $O(N)$ paired elements.

## TypeScript Implementation

```typescript
export class MinStack {
  private stack: { val: number; min: number }[] = [];

  push(val: number): void {
    const currentMin = this.stack.length === 0 ? val : Math.min(val, this.getMin());
    this.stack.push({ val, min: currentMin });
  }

  pop(): void {
    this.stack.pop();
  }

  top(): number {
    return this.stack[this.stack.length - 1].val;
  }

  getMin(): number {
    return this.stack[this.stack.length - 1].min;
  }
}
```

## Rust Implementation

```rust
pub struct MinStack {
    stack: Vec<(i32, i32)>,
}

impl MinStack {
    pub fn new() -> Self {
        Self { stack: Vec::new() }
    }

    pub fn push(&mut self, val: i32) {
        let current_min = match self.stack.last() {
            Some(&(_, min)) => min.min(val),
            None => val,
        };
        self.stack.push((val, current_min));
    }

    pub fn pop(&mut self) {
        self.stack.pop();
    }

    pub fn top(&self) -> i32 {
        self.stack.last().unwrap().0
    }

    pub fn get_min(&self) -> i32 {
        self.stack.last().unwrap().1
    }
}
```
