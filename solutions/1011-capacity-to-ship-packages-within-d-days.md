# 1011. Capacity To Ship Packages Within D Days

## Complexity
- Time Complexity: O(n * log(sum(weights)))
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn ship_within_days(weights: Vec<i32>, days: i32) -> i32 {
    let mut left = *weights.iter().max().unwrap();
    let mut right: i32 = weights.iter().sum();

    let feasible = |cap: i32| -> bool {
        let mut d = 1;
        let mut current = 0;
        for &w in &weights {
            if current + w > cap {
                d += 1;
                current = 0;
            }
            current += w;
        }
        d <= days
    };

    while left < right {
        let mid = left + (right - left) / 2;
        if feasible(mid) {
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
export function shipWithinDays(weights: number[], days: number): number {
    let left = Math.max(...weights);
    let right = weights.reduce((acc, cur) => acc + cur, 0);

    const feasible = (cap: number): boolean => {
        let d = 1, current = 0;
        for (const w of weights) {
            if (current + w > cap) {
                d++;
                current = 0;
            }
            current += w;
        }
        return d <= days;
    };

    while (left < right) {
        const mid = Math.floor(left + (right - left) / 2);
        if (feasible(mid)) right = mid;
        else left = mid + 1;
    }

    return left;
}
```
