# 1046. Last Stone Weight

## Problem Statement
You are given an array of integers `stones` where `stones[i]` is the weight of the `i-th` stone.

We are playing a game with the stones. On each turn, we choose the **heaviest two stones** and smash them together. Suppose the heaviest two stones have weights `x` and `y` with `x <= y`. The result of this smash is:
- If `x == y`, both stones are destroyed.
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left.

Return the weight of the last remaining stone. If there are no stones left, return `0`.

---

## TypeScript Implementation

```typescript
export function lastStoneWeight(stones: number[]): number {
  stones.sort((a, b) => a - b);

  while (stones.length > 1) {
    const y = stones.pop()!;
    const x = stones.pop()!;

    if (x !== y) {
      const diff = y - x;
      // Binary search insert
      let low = 0;
      let high = stones.length;
      while (low < high) {
        const mid = (low + high) >> 1;
        if (stones[mid] < diff) {
          low = mid + 1;
        } else {
          high = mid;
        }
      }
      stones.splice(low, 0, diff);
    }
  }

  return stones.length === 1 ? stones[0] : 0;
}
```

---

## Rust Implementation

```rust
use std::collections::BinaryHeap;

pub struct Solution;

impl Solution {
    pub fn last_stone_weight(stones: Vec<i32>) -> i32 {
        let mut heap: BinaryHeap<i32> = BinaryHeap::from(stones);

        while heap.len() > 1 {
            let y = heap.pop().unwrap();
            let x = heap.pop().unwrap();

            if x != y {
                heap.push(y - x);
            }
        }

        heap.pop().unwrap_or(0)
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(n log n)` with `n` heap pop and push operations.
- Space Complexity: `O(n)` to store stones in binary heap.
