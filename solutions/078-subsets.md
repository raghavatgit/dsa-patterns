# 78. Subsets

## Complexity
- Time Complexity: O(n * 2^n)
- Space Complexity: O(n * 2^n)

## Rust Implementation
```rust
pub fn subsets(nums: Vec<i32>) -> Vec<Vec<i32>> {
    let mut res = Vec::new();
    let mut current = Vec::new();

    fn backtrack(nums: &[i32], start: usize, current: &mut Vec<i32>, res: &mut Vec<Vec<i32>>) {
        res.push(current.clone());
        for i in start..nums.len() {
            current.push(nums[i]);
            backtrack(nums, i + 1, current, res);
            current.pop();
        }
    }

    backtrack(&nums, 0, &mut current, &mut res);
    res
}
```
