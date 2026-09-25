# 56. Merge Intervals

## Problem Statement
Given an array of `intervals` where `intervals[i] = [start_i, end_i]`, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

---

## Method Explanation
1. Sort intervals by their start time: `O(N log N)`.
2. Iterate through the sorted intervals. For each interval:
   - If the merged list is empty or the current interval's start is greater than the previous interval's end, append it as a new disjoint interval.
   - Otherwise, an overlap exists: merge by updating the previous interval's end to `max(prev.end, current.end)`.

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn merge(mut intervals: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        if intervals.is_empty() {
            return vec![];
        }

        intervals.sort_unstable_by_key(|interval| interval[0]);
        let mut merged: Vec<Vec<i32>> = Vec::with_capacity(intervals.len());

        for interval in intervals {
            if merged.is_empty() || merged.last().unwrap()[1] < interval[0] {
                merged.push(interval);
            } else {
                let last = merged.last_mut().unwrap();
                last[1] = last[1].max(interval[1]);
            }
        }

        merged
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_merge_intervals() {
        assert_eq!(
            Solution::merge(vec![vec![1, 3], vec![2, 6], vec![8, 10], vec![15, 18]]),
            vec![vec![1, 6], vec![8, 10], vec![15, 18]]
        );
        assert_eq!(
            Solution::merge(vec![vec![1, 4], vec![4, 5]]),
            vec![vec![1, 5]]
        );
    }
}
```

---

## TypeScript Implementation

```typescript
export function merge(intervals: number[][]): number[][] {
  if (intervals.length === 0) return [];

  intervals.sort((a, b) => a[0] - b[0]);
  const result: number[][] = [intervals[0]];

  for (let i = 1; i < intervals.length; i++) {
    const current = intervals[i];
    const prev = result[result.length - 1];

    if (current[0] <= prev[1]) {
      prev[1] = Math.max(prev[1], current[1]);
    } else {
      result.push(current);
    }
  }

  return result;
}
```

---

## Complexity Analysis
- Time Complexity: `O(N log N)` due to the sorting step.
- Space Complexity: `O(N)` for storing the output intervals (or `O(log N)` auxiliary sorting space).
