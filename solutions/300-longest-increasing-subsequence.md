# 300. Longest Increasing Subsequence

## Complexity
- Time Complexity: O(n log n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn length_of_lis(nums: Vec<i32>) -> i32 {
    let mut tails = Vec::new();

    for x in nums {
        match tails.binary_search(&x) {
            Ok(_) => (),
            Err(idx) => {
                if idx == tails.len() {
                    tails.push(x);
                } else {
                    tails[idx] = x;
                }
            }
        }
    }

    tails.len() as i32
}
```
