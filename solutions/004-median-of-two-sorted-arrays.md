# Problem: Median of Two Sorted Arrays

## Problem Statement
Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays. The overall run time complexity should be $O(\log(m + n))$.

## Intuition & Approach
Binary Search on Partition Index:
1. Ensure `nums1` is the shorter array ($m \le n$) to guarantee binary search runs in $O(\log(\min(m, n)))$.
2. Partition both arrays such that the combined left half contains $(m + n + 1) / 2$ elements.
3. Binary search partition cut $i$ in `nums1` $[0, m]$. Corresponding cut in `nums2` is $j = (m + n + 1) / 2 - i$.
4. Check partition validity:
   - `maxLeft1 <= minRight2` AND `maxLeft2 <= minRight1`.
5. If $i$ is too far right (`maxLeft1 > minRight2`), move binary search left: `high = i - 1`.
6. If $i$ is too far left (`maxLeft2 > minRight1`), move binary search right: `low = i + 1`.
7. Once partition is valid:
   - If total length is odd: $\text{median} = \max(\text{maxLeft1}, \text{maxLeft2})$.
   - If total length is even: $\text{median} = (\max(\text{maxLeft1}, \text{maxLeft2}) + \min(\text{minRight1}, \text{minRight2})) / 2.0$.
8. Time Complexity: $O(\log(\min(M, N)))$. Space Complexity: $O(1)$.

## TypeScript Implementation

```typescript
export function findMedianSortedArrays(nums1: number[], nums2: number[]): number {
  if (nums1.length > nums2.length) {
    return findMedianSortedArrays(nums2, nums1);
  }

  const m = nums1.length;
  const n = nums2.length;
  let low = 0;
  let high = m;

  while (low <= high) {
    const i = (low + high) >> 1;
    const j = ((m + n + 1) >> 1) - i;

    const maxLeft1 = i === 0 ? -Infinity : nums1[i - 1];
    const minRight1 = i === m ? Infinity : nums1[i];

    const maxLeft2 = j === 0 ? -Infinity : nums2[j - 1];
    const minRight2 = j === n ? Infinity : nums2[j];

    if (maxLeft1 <= minRight2 && maxLeft2 <= minRight1) {
      if ((m + n) % 2 === 1) {
        return Math.max(maxLeft1, maxLeft2);
      } else {
        return (Math.max(maxLeft1, maxLeft2) + Math.min(minRight1, minRight2)) / 2;
      }
    } else if (maxLeft1 > minRight2) {
      high = i - 1;
    } else {
      low = i + 1;
    }
  }

  return 0.0;
}
```

## Rust Implementation

```rust
pub fn find_median_sorted_arrays(nums1: Vec<i32>, nums2: Vec<i32>) -> f64 {
    if nums1.len() > nums2.len() {
        return find_median_sorted_arrays(nums2, nums1);
    }

    let m = nums1.len();
    let n = nums2.len();
    let mut low = 0;
    let mut high = m;

    while low <= high {
        let i = (low + high) / 2;
        let j = (m + n + 1) / 2 - i;

        let max_left1 = if i == 0 { i32::MIN } else { nums1[i - 1] };
        let min_right1 = if i == m { i32::MAX } else { nums1[i] };

        let max_left2 = if j == 0 { i32::MIN } else { nums2[j - 1] };
        let min_right2 = if j == n { i32::MAX } else { nums2[j] };

        if max_left1 <= min_right2 && max_left2 <= min_right1 {
            if (m + n) % 2 == 1 {
                return max_left1.max(max_left2) as f64;
            } else {
                return (max_left1.max(max_left2) as f64 + min_right1.min(min_right2) as f64) / 2.0;
            }
        } else if max_left1 > min_right2 {
            high = i - 1;
        } else {
            low = i + 1;
        }
    }

    0.0
}
```
