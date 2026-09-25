# 57. Insert Interval

## Problem Statement
You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [start_i, end_i]` sorted in ascending order by `start_i`. You are also given an interval `newInterval = [start, end]`.

Insert `newInterval` into `intervals` such that `intervals` is still sorted and has no overlapping intervals (merge if necessary).

---

## Method Explanation
A three-phase linear traversal:
1. Append all intervals ending before `newInterval.start`.
2. Merge all intervals overlapping with `newInterval` by expanding `newInterval = [min(start), max(end)]`.
3. Append all remaining intervals starting after the merged `newInterval.end`.

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn insert(intervals: Vec<Vec<i32>>, mut new_interval: Vec<i32>) -> Vec<Vec<i32>> {
        let mut result = Vec::with_capacity(intervals.len() + 1);
        let mut i = 0;
        let n = intervals.len();

        // Phase 1: all intervals before new_interval
        while i < n && intervals[i][1] < new_interval[0] {
            result.push(intervals[i].clone());
            i += 1;
        }

        // Phase 2: merge overlapping intervals
        while i < n && intervals[i][0] <= new_interval[1] {
            new_interval[0] = new_interval[0].min(intervals[i][0]);
            new_interval[1] = new_interval[1].max(intervals[i][1]);
            i += 1;
        }
        result.push(new_interval);

        // Phase 3: all intervals after new_interval
        while i < n {
            result.push(intervals[i].clone());
            i += 1;
        }

        result
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_insert_interval() {
        assert_eq!(
            Solution::insert(vec![vec![1, 3], vec![6, 9]], vec![2, 5]),
            vec![vec![1, 5], vec![6, 9]]
        );
        assert_eq!(
            Solution::insert(
                vec![vec![1, 2], vec![3, 5], vec![6, 7], vec![8, 10], vec![12, 16]],
                vec![4, 8]
            ),
            vec![vec![1, 2], vec![3, 10], vec![12, 16]]
        );
    }
}
```

---

## Complexity Analysis
- Time Complexity: `O(N)` single pass over the sorted array.
- Space Complexity: `O(N)` for the output array.
