# Problem: Koko Eating Bananas

## Problem Statement
Koko loves to eat bananas. There are `n` piles of bananas, the `i`-th pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours. Koko can decide her bananas-per-hour eating speed of `k`. Return the minimum integer `k` such that she can eat all the bananas within `h` hours.

## Intuition & Approach
Binary Search on Answer Space:
1. The search range for eating speed `k` is $[1, \max(\text{piles})]$.
2. Monotonicity condition: If Koko can eat all bananas at speed $k$, she can also finish at any speed $> k$. If she cannot finish at speed $k$, she cannot finish at any speed $< k$.
3. For a candidate speed $m$, hours spent on pile $p$ is $\lceil p / m \rceil = (p + m - 1) / m$.
4. Check if $\sum (p + m - 1) / m \le h$.
5. Binary search converges to minimal valid speed in $O(N \log(\max(\text{piles})))$ time and $O(1)$ space.

## TypeScript Implementation

```typescript
export function minEatingSpeed(piles: number[], h: number): number {
  let low = 1;
  let high = Math.max(...piles);
  let ans = high;

  while (low <= high) {
    const mid = low + Math.floor((high - low) / 2);
    let hoursNeeded = 0;

    for (const pile of piles) {
      hoursNeeded += Math.ceil(pile / mid);
    }

    if (hoursNeeded <= h) {
      ans = mid;
      high = mid - 1; // Seek slower valid eating speed
    } else {
      low = mid + 1;  // Speed too slow, increase lower bound
    }
  }

  return ans;
}
```

## Rust Implementation

```rust
pub fn min_eating_speed(piles: Vec<i32>, h: i32) -> i32 {
    let mut low = 1;
    let mut high = *piles.iter().max().unwrap();
    let mut ans = high;

    while low <= high {
        let mid = low + (high - low) / 2;
        let mut hours_needed: i64 = 0;

        for &p in &piles {
            hours_needed += ((p as i64 + mid as i64 - 1) / mid as i64);
        }

        if hours_needed <= h as i64 {
            ans = mid;
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }

    ans
}
```
