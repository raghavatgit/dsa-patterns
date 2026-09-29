# 560. Subarray Sum Equals K

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::collections::HashMap;

pub fn subarray_sum(nums: Vec<i32>, k: i32) -> i32 {
    let mut count = 0;
    let mut sum = 0;
    let mut map: HashMap<i32, i32> = HashMap::new();
    map.insert(0, 1);
    for num in nums {
        sum += num;
        if let Some(&freq) = map.get(&(sum - k)) {
            count += freq;
        }
        *map.entry(sum).or_insert(0) += 1;
    }
    count
}
```

## TypeScript Implementation
```typescript
export function subarraySum(nums: number[], k: number): number {
    let count = 0;
    let sum = 0;
    const map = new Map<number, number>();
    map.set(0, 1);
    for (const num of nums) {
        sum += num;
        if (map.has(sum - k)) {
            count += map.get(sum - k)!;
        }
        map.set(sum, (map.get(sum) || 0) + 1);
    }
    return count;
}
```
