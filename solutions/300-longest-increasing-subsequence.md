# 300. Longest Increasing Subsequence

## Complexity
- Time Complexity: O(n log n) using patience sorting and binary search
- Space Complexity: O(n) for tails array

## Invariant
`tails[i]` stores the smallest tail of all increasing subsequences of length `i + 1`. The array `tails` is strictly monotonic, enabling binary search for insertion points.

## Rust Implementation
```rust
pub fn length_of_lis(nums: Vec<i32>) -> i32 {
    let mut tails = Vec::new();
    for x in nums {
        match tails.binary_search(&x) {
            Ok(_) => {}, // Duplicate element does not extend strict increasing sequence
            Err(idx) => {
                if idx == tails.len() {
                    tails.push(x);
                } else {
                    tails[idx] = x;
                }
            }
        }
    }
    tails.len() as i32
}
```

## TypeScript Implementation
```typescript
export function lengthOfLIS(nums: number[]): number {
    const tails: number[] = [];
    for (const x of nums) {
        let left = 0;
        let right = tails.length;
        while (left < right) {
            const mid = Math.floor((left + right) / 2);
            if (tails[mid] < x) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        if (left === tails.length) {
            tails.push(x);
        } else {
            tails[left] = x;
        }
    }
    return tails.length;
}
```
