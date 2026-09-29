# 260. Single Number III

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn single_number(nums: Vec<i32>) -> Vec<i32> {
    let diff: i64 = nums.iter().fold(0i64, |acc, &x| acc ^ (x as i64));
    let lowest_bit = diff & -diff;

    let mut a = 0;
    let mut b = 0;

    for x in nums {
        if ((x as i64) & lowest_bit) != 0 {
            a ^= x;
        } else {
            b ^= x;
        }
    }

    vec![a, b]
}
```
