# 853. Car Fleet

## Problem Statement
There are `n` cars at given miles away from the starting mile 0, traveling to reach the destination mile `target`.

You are given two integer arrays `position` and `speed`, both of length `n`, where `position[i]` is the starting position of the `i-th` car and `speed[i]` is the speed of the `i-th` car in miles per hour.

A car can never pass another car ahead of it, but it can catch up to it and drive bumper to bumper at the same speed. The distance between these two cars is ignored: they are assumed to have the same position. A car fleet is some non-empty set of cars driving at the same position and same speed.

Return the number of car fleets that will arrive at the destination.

---

## TypeScript Implementation

```typescript
export function carFleet(target: number, position: number[], speed: number[]): number {
  const n = position.length;
  if (n <= 1) return n;

  const cars = position.map((pos, i) => ({ pos, spd: speed[i] }));
  cars.sort((a, b) => b.pos - a.pos);

  let fleets = 0;
  let prevTime = 0;

  for (const car of cars) {
    const time = (target - car.pos) / car.spd;
    if (time > prevTime) {
      fleets++;
      prevTime = time;
    }
  }

  return fleets;
}
```

---

## Rust Implementation

```rust
pub struct Solution;

impl Solution {
    pub fn car_fleet(target: i32, position: Vec<i32>, speed: Vec<i32>) -> i32 {
        let n = position.len();
        if n <= 1 {
            return n as i32;
        }

        let mut cars: Vec<(i32, f64)> = position
            .into_iter()
            .zip(speed.into_iter())
            .map(|(p, s)| (p, (target - p) as f64 / s as f64))
            .collect();

        cars.sort_unstable_by(|a, b| b.0.cmp(&a.0));

        let mut fleets = 0;
        let mut prev_time = 0.0;

        for (_, time) in cars {
            if time > prev_time {
                fleets += 1;
                prev_time = time;
            }
        }

        fleets
    }
}
```

---

## Complexity Analysis

- Time Complexity: `O(n log n)` to sort cars by descending position.
- Space Complexity: `O(n)` to store paired position and arrival time records.
