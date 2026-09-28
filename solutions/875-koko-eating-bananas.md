# 875. Koko Eating Bananas

## Complexity
- Time Complexity: O(n * log(max(piles)))
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn min_eating_speed(piles: Vec<i32>, h: i32) -> i32 {
    let mut left = 1;
    let mut right = *piles.iter().max().unwrap();

    let can_finish = |speed: i32| -> bool {
        let mut hours = 0i64;
        for &pile in &piles {
            hours += ((pile as i64) + (speed as i64) - 1) / (speed as i64);
        }
        hours <= (h as i64)
    };

    while left < right {
        let mid = left + (right - left) / 2;
        if can_finish(mid) {
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
export function minEatingSpeed(piles: number[], h: number): number {
    let left = 1;
    let right = Math.max(...piles);

    const canFinish = (speed: number): boolean => {
        let hours = 0;
        for (const p of piles) hours += Math.ceil(p / speed);
        return hours <= h;
    };

    while (left < right) {
        const mid = Math.floor(left + (right - left) / 2);
        if (canFinish(mid)) right = mid;
        else left = mid + 1;
    }

    return left;
}
```
