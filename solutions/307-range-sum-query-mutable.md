# Problem: Range Sum Query Mutable (Fenwick Tree)

## Problem Statement
Given an integer array `nums`, handle two types of queries:
1. Update the value of an element at index `index`.
2. Calculate the sum of the elements of `nums` between indices `left` and `right` inclusive.

## Intuition & Approach
Binary Indexed Tree (Fenwick Tree):
1. A Fenwick tree uses an array `tree` of size $N + 1$ (1-indexed).
2. The least significant set bit `i & (-i)` determines the length of the interval covered by `tree[i]`.
3. Prefix sum query `prefix(i)`: Accumulate `tree[i]` and strip lowest set bit `i -= i & (-i)` until $i = 0$. Runs in $O(\log N)$ time.
4. Point update `add(i, delta)`: Add delta to `tree[i]` and advance to parent range `i += i & (-i)` until $i > N$. Runs in $O(\log N)$ time.
5. Range sum `query(left, right)`: `prefix(right + 1) - prefix(left)` in $O(\log N)$ time.
6. Time Complexity: $O(N)$ initialization, $O(\log N)$ per query/update. Space Complexity: $O(N)$.

## TypeScript Implementation

```typescript
export class NumArray {
  private tree: number[];
  private nums: number[];
  private n: number;

  constructor(nums: number[]) {
    this.n = nums.length;
    this.nums = [...nums];
    this.tree = new Array(this.n + 1).fill(0);

    for (let i = 0; i < this.n; i++) {
      this.initAdd(i + 1, nums[i]);
    }
  }

  private initAdd(idx: number, delta: number): void {
    for (let i = idx; i <= this.n; i += i & -i) {
      this.tree[i] += delta;
    }
  }

  update(index: number, val: number): void {
    const delta = val - this.nums[index];
    this.nums[index] = val;
    this.initAdd(index + 1, delta);
  }

  private prefixSum(idx: number): number {
    let sum = 0;
    for (let i = idx; i > 0; i -= i & -i) {
      sum += this.tree[i];
    }
    return sum;
  }

  sumRange(left: number, right: number): number {
    return this.prefixSum(right + 1) - this.prefixSum(left);
  }
}
```

## Rust Implementation

```rust
pub struct NumArray {
    tree: Vec<i32>,
    nums: Vec<i32>,
    n: usize,
}

impl NumArray {
    pub fn new(nums: Vec<i32>) -> Self {
        let n = nums.len();
        let mut tree = vec![0; n + 1];
        let mut bit = Self { tree, nums: nums.clone(), n };

        for (i, &val) in nums.iter().enumerate() {
            bit.add(i + 1, val);
        }
        bit
    }

    fn add(&mut self, mut idx: usize, delta: i32) {
        while idx <= self.n {
            self.tree[idx] += delta;
            idx += idx & (!idx + 1);
        }
    }

    pub fn update(&mut self, index: i32, val: i32) {
        let idx = index as usize;
        let delta = val - self.nums[idx];
        self.nums[idx] = val;
        self.add(idx + 1, delta);
    }

    fn prefix_sum(&self, mut idx: usize) -> i32 {
        let mut sum = 0;
        while idx > 0 {
            sum += self.tree[idx];
            idx -= idx & (!idx + 1);
        }
        sum
    }

    pub fn sum_range(&self, left: i32, right: i32) -> i32 {
        self.prefix_sum(right as usize + 1) - self.prefix_sum(left as usize)
    }
}
```
