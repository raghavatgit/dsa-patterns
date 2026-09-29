# 191. Number of 1 Bits

## Complexity
- Time Complexity: O(k) where k is number of set bits
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn hamming_weight(mut n: i32) -> i32 {
    let mut count = 0;
    while n != 0 {
        n &= n - 1;
        count += 1;
    }
    count
}
```
