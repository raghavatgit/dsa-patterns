# Problem: Product of Array Except Self

## Problem Statement
Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`. You must write an algorithm that runs in $O(N)$ time and without using the division operation.

## Intuition & Approach
For each element `nums[i]`, its total product is:
`answer[i] = (product of elements to left of i) * (product of elements to right of i)`.

1. Pass 1 (Left to Right): Populate `answer[i]` with the running prefix product.
2. Pass 2 (Right to Left): Accumulate running suffix product in a single scalar `suffix`, multiplying into `answer[i]`.

## TypeScript Implementation

```typescript
export function productExceptSelf(nums: number[]): number[] {
  const n = nums.length;
  const answer: number[] = new Array(n).fill(1);

  // Left prefix product pass
  let prefix = 1;
  for (let i = 0; i < n; i++) {
    answer[i] = prefix;
    prefix *= nums[i];
  }

  // Right suffix product pass
  let suffix = 1;
  for (let i = n - 1; i >= 0; i--) {
    answer[i] *= suffix;
    suffix *= nums[i];
  }

  return answer;
}
```

## Rust Implementation

```rust
pub fn product_except_self(nums: &[i32]) -> Vec<i32> {
    let n = nums.len();
    let mut answer = vec![1; n];

    let mut prefix = 1;
    for i in 0..n {
        answer[i] = prefix;
        prefix *= nums[i];
    }

    let mut suffix = 1;
    for i in (0..n).rev() {
        answer[i] *= suffix;
        suffix *= nums[i];
    }

    answer
}
```

## Complexity Analysis
* **Time Complexity:** O(N) two linear passes.
* **Space Complexity:** O(1) auxiliary space (output array does not count toward space complexity).
