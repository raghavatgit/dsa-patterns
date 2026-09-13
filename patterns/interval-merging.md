# Interval Merging Pattern

## Concept
The Interval Merging pattern handles collections of ranges where overlaps must be consolidated. By sorting intervals by their start times, overlapping intervals become consecutive, allowing consolidation in a single linear pass.

Two intervals `A = [startA, endA]` and `B = [startB, endB]` overlap if:
`startB <= endA` (assuming `startA <= startB`).
The merged interval spans `[startA, max(endA, endB)]`.

## TypeScript Implementation

```typescript
export function mergeIntervals(intervals: [number, number][]): [number, number][] {
  if (intervals.length <= 1) return intervals;

  // Sort ascending by start coordinate
  intervals.sort((a, b) => a[0] - b[0]);

  const merged: [number, number][] = [intervals[0]];

  for (let i = 1; i < intervals.length; i++) {
    const current = intervals[i];
    const lastMerged = merged[merged.length - 1];

    if (current[0] <= lastMerged[1]) {
      // Overlap detected: extend the end boundary
      lastMerged[1] = Math.max(lastMerged[1], current[1]);
    } else {
      // Disjoint interval: start a new range
      merged.push(current);
    }
  }

  return merged;
}
```

## Rust Implementation

```rust
pub fn merge_intervals(mut intervals: Vec<(i32, i32)>) -> Vec<(i32, i32)> {
    if intervals.len() <= 1 {
        return intervals;
    }

    intervals.sort_unstable_by_key(|&(start, _)| start);

    let mut merged: Vec<(i32, i32)> = Vec::with_capacity(intervals.len());
    merged.push(intervals[0]);

    for &(start, end) in &intervals[1..] {
        let last = merged.last_mut().unwrap();
        if start <= last.1 {
            last.1 = last.1.max(end);
        } else {
            merged.push((start, end));
        }
    }

    merged
}
```

## Complexity Analysis
* **Time Complexity:** O(N log N) dominated by sorting the input intervals.
* **Space Complexity:** O(N) auxiliary storage for the result list.
