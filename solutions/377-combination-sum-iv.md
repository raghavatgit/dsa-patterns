# 377. Combination Sum IV

## Complexity
- Time Complexity: O(target * len(nums))
- Space Complexity: O(target)

## Rust Implementation
```rust
pub fn combination_sum4(nums: Vec<i32>, target: i32) -> i32 {
    let t = target as usize;
    let mut dp = vec![0u32; t + 1];
    dp[0] = 1;

    for i in 1..=t {
        for &num in &nums {
            let n = num as usize;
            if n <= i {
                dp[i] = dp[i].saturating_add(dp[i - n]);
            }
        }
    }
    dp[t] as i32
}
```
