# 435. Non-overlapping Intervals

## Problem Statement
Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

---

## Greedy Choice Property

To maximize the number of non-overlapping intervals, always select the interval with the earliest ending time (`end`). This leaves the maximum possible room for remaining compatible intervals.

The number of removals is simply `Total Intervals - Maximum Compatible Intervals`.

---

## TypeScript Implementation

```typescript
export function eraseOverlapIntervals(intervals: number[][]): number {
  if (intervals.length === 0) return 0;

  // Sort by ending timestamp ascending
  intervals.sort((a, b) => a[1] - b[1]);

  let nonOverlappingCount = 1;
  let lastEnd = intervals[0][1];

  for (let i = 1; i < intervals.length; i++) {
    const [start, end] = intervals[i];
    if (start >= lastEnd) {
      nonOverlappingCount++;
      lastEnd = end;
    }
  }

  return intervals.length - nonOverlappingCount;
}
```

---

## Rust Implementation

```rust
pub fn erase_overlap_intervals(mut intervals: Vec<Vec<i32>>) -> i32 {
    if intervals.is_empty() {
        return 0;
    }

    // Sort ascending by end time
    intervals.sort_unstable_by_key(|inv| inv[1]);

    let mut compatible_count = 1;
    let mut last_end = intervals[0][1];

    for inv in intervals.iter().skip(1) {
        if inv[0] >= last_end {
            compatible_count += 1;
            last_end = inv[1];
        }
    }

    (intervals.len() - compatible_count) as i32
}
```

---

## Complexity Analysis

* **Time Complexity:** `O(N log N)` dominated by interval sorting. Linear `O(N)` single-pass greedy traversal.
* **Space Complexity:** `O(1)` or `O(log N)` auxiliary stack space for in-place sorting.
