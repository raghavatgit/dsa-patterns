# Prefix Sums Pattern

## Concept
A preprocessing technique where an array `P` is constructed such that `P[i]` stores the cumulative sum of elements from index 0 to `i-1`. This allows any contiguous range sum query `sum(L, R)` to be resolved in O(1) constant time instead of O(N) iteration:

RangeSum(L, R) = P[R + 1] - P[L]

## TypeScript Implementation

```typescript
export class PrefixSumArray {
  private prefix: number[];

  constructor(nums: number[]) {
    this.prefix = new Array(nums.length + 1).fill(0);
    for (let i = 0; i < nums.length; i++) {
      this.prefix[i + 1] = this.prefix[i] + nums[i];
    }
  }

  queryRange(left: number, right: number): number {
    if (left < 0 || right >= this.prefix.length - 1 || left > right) {
      throw new RangeError("Invalid query range boundaries");
    }
    return this.prefix[right + 1] - this.prefix[left];
  }
}
```

## Rust Implementation

```rust
pub struct PrefixSumArray {
    prefix: Vec<i64>,
}

impl PrefixSumArray {
    pub fn new(nums: &[i32]) -> Self {
        let mut prefix = Vec::with_capacity(nums.len() + 1);
        prefix.push(0);

        let mut running_sum: i64 = 0;
        for &num in nums {
            running_sum += num as i64;
            prefix.push(running_sum);
        }

        Self { prefix }
    }

    pub fn query_range(&self, left: usize, right: usize) -> Option<i64> {
        if left > right || right + 1 >= self.prefix.len() {
            return None;
        }
        Some(self.prefix[right + 1] - self.prefix[left])
    }
}
```

## Complexity Analysis
* **Preprocessing Time:** O(N) single-pass array traversal.
* **Query Time:** O(1) direct index arithmetic.
* **Space Complexity:** O(N) auxiliary storage for the prefix array.
