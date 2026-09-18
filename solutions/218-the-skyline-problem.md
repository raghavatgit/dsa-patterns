# Problem: The Skyline Problem

## Problem Statement
A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance. Given the locations and heights of all the buildings, return the skyline formed by these buildings collectively.

## Intuition & Approach
Line Sweep with MultiSet / Max-Heap:
1. Deconstruct each building `[left, right, height]` into two critical point events:
   - Start event at `x = left` with height `height` (marked negative or entering).
   - End event at `x = right` with height `height` (marked positive or exiting).
2. Sort events primarily by $x$-coordinate. Tie-breaking:
   - If two start events share $x$, process larger height first.
   - If two end events share $x$, process smaller height first.
   - If a start and end event share $x$, process start event first.
3. Maintain an active multiset / priority queue of building heights.
4. When processing an event:
   - Start event: insert height into active collection.
   - End event: remove height from active collection.
   - If the maximum height among active buildings changes, record `[x, current_max_height]` as a skyline vertex.
5. Time Complexity: $O(N \log N)$. Space Complexity: $O(N)$ heap storage.

## TypeScript Implementation

```typescript
export function getSkyline(buildings: number[][]): number[][] {
  const events: [number, number][] = [];

  for (const [l, r, h] of buildings) {
    events.push([l, -h]); // Entering building
    events.push([r, h]);  // Exiting building
  }

  // Sort critical points with invariant tie-breaking
  events.sort((a, b) => {
    if (a[0] !== b[0]) return a[0] - b[0];
    return a[1] - b[1];
  });

  const result: number[][] = [];
  const heights: number[] = [0]; // Active heights
  let prevMax = 0;

  for (const [x, h] of events) {
    if (h < 0) {
      // Add building height
      heights.push(-h);
      heights.sort((a, b) => a - b);
    } else {
      // Remove building height
      const idx = heights.indexOf(h);
      if (idx !== -1) heights.splice(idx, 1);
    }

    const currentMax = heights[heights.length - 1];
    if (currentMax !== prevMax) {
      result.push([x, currentMax]);
      prevMax = currentMax;
    }
  }

  return result;
}
```
