# 525. Contiguous Array

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n)

## Rust Implementation
```rust
use std::collections::HashMap;

pub fn find_max_length(nums: Vec<i32>) -> i32 {
    let mut map: HashMap<i32, i32> = HashMap::new();
    map.insert(0, -1);
    let mut max_len = 0;
    let mut count = 0;
    for (i, &num) in nums.iter().enumerate() {
        count += if num == 1 { 1 } else { -1 };
        if let Some(&prev_idx) = map.get(&count) {
            max_len = max_len.max(i as i32 - prev_idx);
        } else {
            map.insert(count, i as i32);
        }
    }
    max_len
}
```

## TypeScript Implementation
```typescript
export function findMaxLength(nums: number[]): number {
    const map = new Map<number, number>();
    map.set(0, -1);
    let maxLen = 0;
    let count = 0;
    for (let i = 0; i < nums.length; i++) {
        count += nums[i] === 1 ? 1 : -1;
        if (map.has(count)) {
            maxLen = Math.max(maxLen, i - map.get(count)!);
        } else {
            map.set(count, i);
        }
    }
    return maxLen;
}
```
