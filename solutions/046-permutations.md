# 46. Permutations

## Complexity
- Time Complexity: O(n * n!)
- Space Complexity: O(n!)

## Rust Implementation
```rust
pub fn permute(mut nums: Vec<i32>) -> Vec<Vec<i32>> {
    let mut res = Vec::new();

    fn backtrack(nums: &mut [i32], start: usize, res: &mut Vec<Vec<i32>>) {
        if start == nums.len() {
            res.push(nums.to_vec());
            return;
        }
        for i in start..nums.len() {
            nums.swap(start, i);
            backtrack(nums, start + 1, res);
            nums.swap(start, i);
        }
    }

    backtrack(&mut nums, 0, &mut res);
    res
}
```
