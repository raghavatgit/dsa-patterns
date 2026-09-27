# 219. Contains Duplicate II

## Problem Statement
Given an integer array `nums` and an integer `k`, return `true` if there are two distinct indices `i` and `j` such that `nums[i] == nums[j]` and `abs(i - j) <= k`.

---

## TypeScript Implementation

```typescript
export function containsNearbyDuplicate(nums: number[], k: number): boolean {
  const set = new Set<number>();

  for (let i = 0; i < nums.length; i++) {
    if (set.has(nums[i])) return true;
    set.add(nums[i]);
    if (set.size > k) {
      set.delete(nums[i - k]);
    }
  }

  return false;
}
```

---

## Complexity Analysis
* **Time Complexity:** O(N).
* **Space Complexity:** O(min(N, k)) sliding set.
