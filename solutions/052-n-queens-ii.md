# 52. N-Queens II

## Complexity
- Time Complexity: O(N!)
- Space Complexity: O(N)

## Rust Implementation
```rust
pub fn total_n_queens(n: i32) -> i32 {
    let mut count = 0;

    fn solve(row: i32, n: i32, cols: i32, d1: i32, d2: i32, count: &mut i32) {
        if row == n {
            *count += 1;
            return;
        }
        let available = ((1 << n) - 1) & !(cols | d1 | d2);
        let mut bits = available;
        while bits > 0 {
            let p = bits & -bits;
            bits -= p;
            solve(row + 1, n, cols | p, (d1 | p) << 1, (d2 | p) >> 1, count);
        }
    }

    solve(0, n, 0, 0, 0, &mut count);
    count
}
```
