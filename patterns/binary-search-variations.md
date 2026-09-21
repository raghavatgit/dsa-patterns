# Pattern: Binary Search Invariants and Monotonic Predicates

## Overview
Binary Search extends far beyond searching sorted arrays: it optimizes any monotonic decision problem $P(x) \in \{\text{true}, \text{false}\}$ where:
$$\forall y > x, P(x) \implies P(y)$$

## Universal Template (Left-Biased Mid)
```typescript
function binarySearchFirstTrue(low: number, high: number, predicate: (val: number) => boolean): number {
  let ans = -1;
  while (low <= high) {
    const mid = low + Math.floor((high - low) / 2);
    if (predicate(mid)) {
      ans = mid;
      high = mid - 1; // Seek earlier valid point
    } else {
      low = mid + 1;  // Increase search lower bound
    }
  }
  return ans;
}
```
