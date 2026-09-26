# 347. Top K Frequent Elements

## Problem Statement
Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in any order. The algorithm must have time complexity better than `O(N log N)`.

---

## Optimal Architecture: Bucket Sort by Frequency

1. Count frequencies using a hash map in `O(N)` time.
2. Initialize an array of buckets where index represents frequency count (ranging from `0` to `N`).
3. Iterate buckets backwards from `N` down to `1` collecting elements until `k` items are accumulated.

This achieves strict linear `O(N)` time without relying on a min-heap `O(N log K)`.

---

## TypeScript Implementation

```typescript
export function topKFrequent(nums: number[], k: number): number[] {
  const freqMap = new Map<number, number>();
  for (const num of nums) {
    freqMap.set(num, (freqMap.get(num) || 0) + 1);
  }

  const buckets: number[][] = Array.from({ length: nums.length + 1 }, () => []);
  for (const [num, freq] of freqMap.entries()) {
    buckets[freq].push(num);
  }

  const result: number[] = [];
  for (let f = buckets.length - 1; f >= 0 && result.length < k; f--) {
    if (buckets[f].length > 0) {
      for (const num of buckets[f]) {
        result.push(num);
        if (result.length === k) break;
      }
    }
  }

  return result;
}
```

---

## Rust Implementation

```rust
use std::collections::HashMap;

pub fn top_k_frequent(nums: Vec<i32>, k: i32) -> Vec<i32> {
    let mut freq_map: HashMap<i32, usize> = HashMap::with_capacity(nums.len());
    for &num in &nums {
        *freq_map.entry(num).or_insert(0) += 1;
    }

    let mut buckets: Vec<Vec<i32>> = vec![Vec::new(); nums.len() + 1];
    for (&num, &freq) in &freq_map {
        buckets[freq].push(num);
    }

    let mut result = Vec::with_capacity(k as usize);
    for bucket in buckets.into_iter().rev() {
        for num in bucket {
            result.push(num);
            if result.len() == k as usize {
                return result;
            }
        }
    }

    result
}
```

---

## Complexity Analysis

* **Time Complexity:** `O(N)` linear time across frequency counting, bucket assignment, and reverse scanning.
* **Space Complexity:** `O(N)` auxiliary storage for frequency map and bucket arrays.
