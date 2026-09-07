# Two Pointers Pattern

## Concept
Using two pointers converging from opposing boundaries allows searching sorted spaces with O(1) auxiliary space, replacing quadratic O(N^2) brute-force searches.

## TypeScript Implementation

```typescript
export function twoSumSorted(numbers: number[], target: number): [number, number] | null {
  let left = 0;
  let right = numbers.length - 1;

  while (left < right) {
    const sum = numbers[left] + numbers[right];
    if (sum === target) {
      return [left + 1, right + 1]; // 1-indexed
    } else if (sum < target) {
      left++;
    } else {
      right--;
    }
  }

  return null;
}
```

## Rust Implementation

```rust
pub fn two_sum_sorted(numbers: &[i32], target: i32) -> Option<(usize, usize)> {
    let mut left = 0;
    let mut right = numbers.len().checked_sub(1)?;

    while left < right {
        let sum = numbers[left] + numbers[right];
        if sum == target {
            return Some((left + 1, right + 1));
        } else if sum < target {
            left += 1;
        } else {
            right -= 1;
        }
    }

    None
}
```
