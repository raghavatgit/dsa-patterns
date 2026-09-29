# 494. Target Sum

## Complexity
- Time Complexity: O(n * subset_target)
- Space Complexity: O(subset_target)

## Rust Implementation
```rust
pub fn find_target_sum_ways(nums: Vec<i32>, target: i32) -> i32 {
    let sum: i32 = nums.iter().sum();
    if (sum + target) % 2 != 0 || sum < target.abs() { return 0; }
    let s = ((sum + target) / 2) as usize;

    let mut dp = vec![0; s + 1];
    dp[0] = 1;

    for num in nums {
        let n = num as usize;
        for j in (n..=s).rev() {
            dp[j] += dp[j - n];
        }
    }
    dp[s]
}
```
