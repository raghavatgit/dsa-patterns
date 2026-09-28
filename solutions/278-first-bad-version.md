# 278. First Bad Version

## Complexity
- Time Complexity: O(log n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn first_bad_version(n: i32, is_bad: impl Fn(i32) -> bool) -> i32 {
    let mut left = 1;
    let mut right = n;

    while left < right {
        let mid = left + (right - left) / 2;
        if is_bad(mid) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    left
}
```

## TypeScript Implementation
```typescript
export function solution(isBadVersion: (version: number) => boolean) {
    return function(n: number): number {
        let left = 1, right = n;
        while (left < right) {
            const mid = Math.floor(left + (right - left) / 2);
            if (isBadVersion(mid)) right = mid;
            else left = mid + 1;
        }
        return left;
    };
}
```
