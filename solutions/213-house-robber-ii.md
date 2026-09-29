# 213. House Robber II

## Complexity
- Time Complexity: O(n)
- Space Complexity: O(1)

## Rust Implementation
```rust
pub fn rob(nums: Vec<i32>) -> i32 {
    if nums.len() == 1 { return nums[0]; }
    fn rob_linear(slice: &[i32]) -> i32 {
        let mut r1 = 0;
        let mut r2 = 0;
        for &n in slice {
            let tmp = r2.max(r1 + n);
            r1 = r2;
            r2 = tmp;
        }
        r2
    }
    let n = nums.len();
    rob_linear(&nums[..n - 1]).max(rob_linear(&nums[1..]))
}
```
