# 78. Subsets

## Complexity
- Time Complexity: O(n * 2^n)
- Space Complexity: O(n)

## Rust Implementation
```rust
pub fn subsets(nums: Vec<i32>) -> Vec<Vec<i32>> {
    let mut res = Vec::new();
    let mut subset = Vec::new();

    fn dfs(nums: &[i32], idx: usize, subset: &mut Vec<i32>, res: &mut Vec<Vec<i32>>) {
        if idx == nums.len() {
            res.push(subset.clone());
            return;
        }
        subset.push(nums[idx]);
        dfs(nums, idx + 1, subset, res);
        subset.pop();
        dfs(nums, idx + 1, subset, res);
    }

    dfs(&nums, 0, &mut subset, &mut res);
    res
}
```
