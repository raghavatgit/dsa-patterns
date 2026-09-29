# 128. Longest Consecutive Sequence

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(n) for HashSet lookup

## Rust Implementation
```rust
use std::collections::HashSet;

pub fn longest_consecutive(nums: Vec<i32>) -> i32 {
    let set: HashSet<i32> = nums.into_iter().collect();
    let mut longest = 0;

    for &num in &set {
        if !set.contains(&(num - 1)) {
            let mut curr = num;
            let mut streak = 1;
            while set.contains(&(curr + 1)) {
                curr += 1;
                streak += 1;
            }
            longest = longest.max(streak);
        }
    }
    longest
}
```

## TypeScript Implementation
```typescript
export function longestConsecutive(nums: number[]): number {
    const set = new Set(nums);
    let longest = 0;

    for (const num of set) {
        if (!set.has(num - 1)) {
            let current = num;
            let streak = 1;
            while (set.has(current + 1)) {
                current += 1;
                streak += 1;
            }
            longest = Math.max(longest, streak);
        }
    }
    return longest;
}
```
